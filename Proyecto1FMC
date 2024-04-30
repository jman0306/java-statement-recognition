/*
Juan Manuel Ambriz Núñez
Fundamentos Matemáticos de la Comoutación
18/04/2024
*/

################################################### BIBLIOTECAS NECESARIAS ###################################################

import pip

pip.main(['install', '--upgrade','tkinter'])
pip.main(['install', '--upgrade','os'])
pip.main(['install', '--upgrade','shutil'])
pip.main(['install', '--upgrade','regex'])

################################################### IMPORTS NECESARIOS ###################################################

import tkinter as tk
from tkinter import filedialog
import os
import shutil
import re

################################################### CARGA DE ARCHIVO TXT ###################################################

def cargar_archivo():
    
    ruta_archivo = filedialog.askopenfilename(initialdir=os.getcwd(), title="Seleccionar archivo", filetypes=(("Archivos de texto", "*.txt"), ("Todos los archivos", "*.*")))
    if ruta_archivo:           
        with open(ruta_archivo, 'r') as archivo:                     
            nombre_archivo = os.path.basename(ruta_archivo) # Obtienes el nombre del archivo
            nombre_nuevo_archivo = "JAVA.txt"               # Cambia el nombre para que siempre sea el mismo y poderlo usar en el programa
            shutil.copy(ruta_archivo, nombre_nuevo_archivo) # Copias el archivo a la carpeta actual
            print("Archivo cargado con éxito")
        archivo.close()
             
        ventana.destroy()  

# Crear ventana principal
ventana = tk.Tk()
ventana.title("Cargar archivo de texto")

# Botón para cargar archivo
boton_cargar = tk.Button(ventana, text="Cargar archivo", command=cargar_archivo)
boton_cargar.pack()

# Ejecutar el bucle de eventos
ventana.mainloop()

################################################### REACOMODO DE ARCHIVO ###################################################

carpeta_actual = os.getcwd()
ruta_documento = os.path.join(carpeta_actual, "JAVA.txt")

with open(ruta_documento, 'r') as archivo:
    contenido = archivo.read()
archivo.close()
    
nuevo_contenido = re.sub(r'\s+', '', contenido)
nombre_archivo = os.path.basename(ruta_documento)

with open(ruta_documento, 'w') as nuevo_archivo:
    nuevo_archivo.write(nuevo_contenido)
nuevo_archivo.close()


print("Archivo modificado con éxito")

################################################### CONTANDO OCURRENCIAS ###################################################

#---------------------------------------------------------INTS--------------------------------------------------------------

# Se buscan todas las subcadenas que cumplan con la expresion regular encontrada para detectar las siguientes cadenas:
# int entero1;
# int entero2, entero3, entero4;
# int entero5 = 10;
# int entero6 = 10, entero7 = 20, entero8 = 30;
ocurrencias_ints = re.findall(r'int[a-zA-Z][a-zA-Z0-9_]*(?:=-?\d+)?(?:,[a-zA-Z][a-zA-Z0-9_]*(?:=-?\d+)*)*;', nuevo_contenido)
# Se cuentan las variables declaradas del arreglo obtenido con las coincidencias que encontró la funcion regex
# Las cuenta tomando en cuenta que si no hay ',' es una variable y, en el caso contrario, son el número de ',' + 1
ints_declarados = 0
for ocurrencia in ocurrencias_ints:
    if ',' in ocurrencia:
        ints_declarados += ocurrencia.count(',') + 1
    else:
        ints_declarados += 1
# Se cuentan las variables inicializadas del arreglo obtenido con las coincidencias que encontró la funcion regex
# Las cuenta encontrando el número de '=' que encuentra       
ints_inicializados = 0
for ocurrencia in ocurrencias_ints:
    if '=' in ocurrencia:
        ints_inicializados += ocurrencia.count('=')
# Se guarda el nombre de las variables en dos grupos, declaradas e inicializadas
vars_ints_ini = []
vars_ints_dec = []
vars_ints_dec_aux = []
vars_ints_ini_aux = []
for ocurrencia in ocurrencias_ints:
    vars_ints_dec_aux.extend(re.findall(r'int[a-zA-Z][a-zA-Z0-9_]*,|[a-zA-Z][a-zA-Z0-9_]*;|[a-zA-Z][a-zA-Z0-9_]*,|int[a-zA-Z][a-zA-Z0-9_]*;', ocurrencia))
    vars_ints_ini_aux.extend(re.findall(r'int[a-zA-Z][a-zA-Z0-9_]*=|,[a-zA-Z][a-zA-Z0-9_]*=', ocurrencia))
# Se le quita el "int", si está sólo al principio de la subcadena, y los símbolos para que quede el nombre de la variable
vars_ints_dec = [re.sub(r'^int|[\W_]+', '', elemento) for elemento in vars_ints_dec_aux]
vars_ints_ini = [re.sub(r'^int|[\W_]+', '', elemento) for elemento in vars_ints_ini_aux]

#-----------------------------------------------------INTS_ARREGLO-----------------------------------------------------------

# Se buscan todas las subcadenas que cumplan con la expresion regular encontrada para detectar las siguientes cadenas:
# int[] arregloEnteros1;
# int[] arregloEnteros2, arregloEnteros3, arregloEnteros4;
# int[] arregloEnteros5 = new int [3];
# int[] arregloEnteros6 = new int[4], arregloEnteros7 = new int[5];
# int[] arregloEnteros8 = {1, 2, 3, 4, 5};
# int[] arregloEnteros9 = {1, 2, 3, 4, 5}, arregloEnteros10 = {6, 7, 8, 9, 10};
ocurrencias_ints_array = re.findall(r'int\[\][a-zA-Z][a-zA-Z0-9_]*(?:=newint\[\d+\])?(?:,[a-zA-Z][a-zA-Z0-9_]*(?:=newint\[\d+\])*)*;', nuevo_contenido)
# Se agrega una nueva función regex para encontrar los casos en donde se inicializa la variable de la siguiente manera "int[] arregloEnteros8 = {1, 2, 3, 4, 5};"
ocurrencias_ints_array_aux = re.findall(r'int\[\][a-zA-Z][a-zA-Z0-9_]*=\{-?\d+(?:,-?\d+)*\}(?:,[a-zA-Z][a-zA-Z0-9_]*=\{-?\d+(?:,-?\d+)*\})*;', nuevo_contenido)
# Se extiende el arreglo para agregar los casos encontrados en la segunda función regex
ocurrencias_ints_array.extend(ocurrencias_ints_array_aux)
# Se cuentan las variables declaradas del arreglo obtenido con las coincidencias que encontró la función regex
# Las cuenta encontrando '{' dentro de la subcadena, si es que hay y, en el caso de que no haya, cuenta ',' + 1 
ints_array_declarados = 0
for ocurrencia in ocurrencias_ints_array:
    if '{' in ocurrencia:
        ints_array_declarados += ocurrencia.count('{')
    elif ',' in ocurrencia:
        ints_array_declarados += ocurrencia.count(',') + 1
    else:
        ints_array_declarados += 1
# Se cuentan las variables inicializadas del arreglo obtenido con las coincidencias que encontró la función regex
# Las cuenta encontrando '{' y '[', pero en el caso '[' se resta 1 para no contar el de la declaración inicial "int[]"   
ints_array_inicializados = 0
for ocurrencia in ocurrencias_ints_array:
    if '[' in ocurrencia and ocurrencia.count('[')>1 or '{' in ocurrencia:
        ints_array_inicializados += ocurrencia.count('[') -1
        ints_array_inicializados += ocurrencia.count('{')
# Se guarda el nombre de las variables en dos grupos, declaradas e inicializadas
vars_ints_array_ini = []
vars_ints_array_dec = []
vars_ints_dec_array_aux = []
vars_ints_ini_array_aux = []
for ocurrencia in ocurrencias_ints_array:
    vars_ints_dec_array_aux.extend(re.findall(r'int\[\][a-zA-Z][a-zA-Z0-9_]*,|[a-zA-Z][a-zA-Z0-9_]*;|[a-zA-Z][a-zA-Z0-9_]*,|int\[\][a-zA-Z][a-zA-Z0-9_]*;', ocurrencia))
    vars_ints_ini_array_aux.extend(re.findall(r'int\[\][a-zA-Z][a-zA-Z0-9_]*=|,[a-zA-Z][a-zA-Z0-9_]*=', ocurrencia))
# Se le quita el "int[]", si está sólo al principio de la subcadena, y los símbolos para que quede el nombre de la variable
vars_ints_array_dec = [re.sub(r'^int|[\W_]+', '', elemento) for elemento in vars_ints_dec_array_aux]
vars_ints_array_ini = [re.sub(r'^int|[\W_]+', '', elemento) for elemento in vars_ints_ini_array_aux]

#-----------------------------------------------------STRING-----------------------------------------------------------

# Se buscan todas las subcadenas que cumplan con la expresion regular encontrada para detectar las siguientes cadenas:
# String cadena1;
# String cadena2, cadena3, cadena4;
# String cadena5 = "Hola mundo";
# String cadena6 = "Hola1", cadena7 = "Hola2";
ocurrencias_strings_aux = re.findall(r'(String[a-zA-Z][a-zA-Z0-9_]*(?:="([^"]+)")?(?:,[a-zA-Z][a-zA-Z0-9_]*(?:="([^"]+)")*)*;)', nuevo_contenido)
# Se realiza lo siguiente para seleccionar solo el primer elemento de cada sublista por el formato en que regresa las ocurrencias
# [('Stringcadena1;', '', ''), ('Stringcadena2,cadena3,cadena4;', '', ''), ('Stringcadena5="Holamundo";', 'Holamundo', ''), ('Stringcadena6="Hola1",cadena7="Hola2";', 'Hola1', 'Hola2')]
ocurrencias_strings = [sublista[0] for sublista in ocurrencias_strings_aux]
# Se cuentan las variables declaradas del arreglo obtenido con las coincidencias que encontró la funcion regex
# Las cuenta tomando en cuenta que si no hay ',' es una variable y, en el caso contrario, son el número de ',' + 1
strings_declarados = 0
for ocurrencia in ocurrencias_strings:
    if ',' in ocurrencia:
        strings_declarados += ocurrencia.count(',') + 1
    else:
        strings_declarados += 1
# Se cuentan las variables inicializadas del arreglo obtenido con las coincidencias que encontró la funcion regex
# Las cuenta encontrando el número de '=' que encuentra 
strings_inicializados = 0
for ocurrencia in ocurrencias_strings:
    if '=' in ocurrencia:
        strings_inicializados += ocurrencia.count('=')
# Se guarda el nombre de las variables en dos grupos, declaradas e inicializadas
vars_strings_ini = []
vars_strings_dec = []
vars_strings_dec_aux = []
vars_strings_ini_aux = []
for ocurrencia in ocurrencias_strings:
    vars_strings_dec_aux.extend(re.findall(r'String[a-zA-Z][a-zA-Z0-9_]*,|[a-zA-Z][a-zA-Z0-9_]*;|[a-zA-Z][a-zA-Z0-9_]*,|String[a-zA-Z][a-zA-Z0-9_]*;', ocurrencia))
    vars_strings_ini_aux.extend(re.findall(r'String[a-zA-Z][a-zA-Z0-9_]*=|,[a-zA-Z][a-zA-Z0-9_]*=', ocurrencia))
# Se le quita el "String", si está sólo al principio de la subcadena, y los símbolos para que quede el nombre de la variable
vars_strings_dec = [re.sub(r'^String|[\W_]+', '', elemento) for elemento in vars_strings_dec_aux]
vars_strings_ini = [re.sub(r'^String|[\W_]+', '', elemento) for elemento in vars_strings_ini_aux]

#-----------------------------------------------------STRING_ARREGLO-----------------------------------------------------------1

# Se buscan todas las subcadenas que cumplan con la expresion regular encontrada para detectar las siguientes cadenas:
# String[] arregloCadena1;
# String[] arregloCadena2, arregloCadena3, arregloCadena4;
# String[] arregloCadena5 = new String[3];
# String[] arregloCadena6 = new String[4], arregloCadena7 = new String[5];
# String[] arregloCadena8 = {"hola", "es", "arreglo"};
# String[] arregloCadena9 = {"hola1", "es1", "arreglo1"}, arregloCadena10 = {"hola2", "es2", "arreglo2"};
ocurrencias_strings_array = re.findall(r'(String\[\][a-zA-Z][a-zA-Z0-9_]*(?:=newString\[\d+\])?(?:,[a-zA-Z][a-zA-Z0-9_]*(?:=newString\[\d+\])*)*;)', nuevo_contenido)
# Se agrega una nueva función regex para encontrar los casos en donde se inicializa la variable de la siguiente manera "String[] arregloCadena8 = {"hola", "es", "arreglo"};"
ocurrencias_strings_array_aux1 = re.findall(r'(String\[\][a-zA-Z][a-zA-Z0-9_]*=\{"([^"]+)"(?:,"([^"]+)")*\}(?:,[a-zA-Z][a-zA-Z0-9_]*=\{"([^"]+)"(?:,"([^"]+)")*\})*;)', nuevo_contenido)
# Se realiza lo siguiente para seleccionar solo el primer elemento de cada sublista por el formato en que regresa las ocurrencias
# [('String[]arregloCadena8={"hola","es","arreglo"};', 'hola', 'arreglo', '', ''), ('String[]arregloCadena9={"hola1","es1","arreglo1"},arregloCadena10={"hola2","es2","arreglo2"};', 'hola1', 'arreglo1', 'hola2', 'arreglo2')]
ocurrencias_strings_array_aux = [sublista[0] for sublista in ocurrencias_strings_array_aux1]
# Se extiende el arreglo para agregar los casos encontrados en la segunda función regex
ocurrencias_strings_array.extend(ocurrencias_strings_array_aux)
# Se cuentan las variables declaradas del arreglo obtenido con las coincidencias que encontró la función regex
# Las cuenta encontrando '{' dentro de la subcadena, si es que hay y, en el caso de que no haya, cuenta ',' + 1                    
strings_array_declarados = 0
for ocurrencia in ocurrencias_strings_array:
    if '{' in ocurrencia:
        strings_array_declarados += ocurrencia.count('{')
    elif ',' in ocurrencia:
        strings_array_declarados += ocurrencia.count(',') + 1
    else:
        strings_array_declarados += 1
# Se cuentan las variables inicializadas del arreglo obtenido con las coincidencias que encontró la función regex
# Las cuenta encontrando '{' y '[', pero en el caso '[' se resta 1 para no contar el de la declaración inicial "String[]"       
strings_array_inicializados = 0
for ocurrencia in ocurrencias_strings_array:
    if '[' in ocurrencia and ocurrencia.count('[')>1 or '{' in ocurrencia:
        strings_array_inicializados += ocurrencia.count('[') -1
        strings_array_inicializados += ocurrencia.count('{')
# Se guarda el nombre de las variables en dos grupos, declaradas e inicializadas
vars_strings_array_ini = []
vars_strings_array_dec = []
vars_strings_dec_array_aux = []
vars_strings_ini_array_aux = []
for ocurrencia in ocurrencias_strings_array:
    vars_strings_dec_array_aux.extend(re.findall(r'String\[\][a-zA-Z][a-zA-Z0-9_]*,|[a-zA-Z][a-zA-Z0-9_]*;|[a-zA-Z][a-zA-Z0-9_]*,|String\[\][a-zA-Z][a-zA-Z0-9_]*;', ocurrencia))
    vars_strings_ini_array_aux.extend(re.findall(r'String\[\][a-zA-Z][a-zA-Z0-9_]*=|,[a-zA-Z][a-zA-Z0-9_]*=', ocurrencia))
# Se le quita el "String[]", si está sólo al principio de la subcadena, y los símbolos para que quede el nombre de la variable
vars_strings_array_dec = [re.sub(r'^String|[\W_]+', '', elemento) for elemento in vars_strings_dec_array_aux]
vars_strings_array_ini = [re.sub(r'^String|[\W_]+', '', elemento) for elemento in vars_strings_ini_array_aux]

#-----------------------------------------------------FLOAT-----------------------------------------------------------

# Se buscan todas las subcadenas que cumplan con la expresion regular encontrada para detectar las siguientes cadenas:
# float decimal1;
# float decimal2, decimal3, decmal4;
# float decimal5 = 10.0f;
# float decimal6 = 10.0f, decimal7 = 20.0f, decimal8 = 30.0f;
ocurrencias_floats = re.findall(r'float[a-zA-Z][a-zA-Z0-9_]*(?:=-?\d+\.\d+f)?(?:,[a-zA-Z][a-zA-Z0-9_]*(?:=-?\d+\.\d+f)*)*;', nuevo_contenido)
# Se cuentan las variables declaradas del arreglo obtenido con las coincidencias que encontró la funcion regex
# Las cuenta tomando en cuenta que si no hay ',' es una variable y, en el caso contrario, son el número de ',' + 1
floats_declarados = 0
for ocurrencia in ocurrencias_floats:
    if ',' in ocurrencia:
        floats_declarados += ocurrencia.count(',') + 1
    else:
        floats_declarados += 1
# Se cuentan las variables inicializadas del arreglo obtenido con las coincidencias que encontró la funcion regex
# Las cuenta encontrando el número de '=' que encuentra        
floats_inicializados = 0
for ocurrencia in ocurrencias_floats:
    if '=' in ocurrencia:
        floats_inicializados += ocurrencia.count('=')
# Se guarda el nombre de las variables en dos grupos, declaradas e inicializadas
vars_floats_ini = []
vars_floats_dec = []
vars_floats_dec_aux = []
vars_floats_ini_aux = []
for ocurrencia in ocurrencias_floats:
    vars_floats_dec_aux.extend(re.findall(r'float[a-zA-Z][a-zA-Z0-9_]*,|[a-zA-Z][a-zA-Z0-9_]*;|[a-zA-Z][a-zA-Z0-9_]*,|float[a-zA-Z][a-zA-Z0-9_]*;', ocurrencia))
    vars_floats_ini_aux.extend(re.findall(r'float[a-zA-Z][a-zA-Z0-9_]*=|,[a-zA-Z][a-zA-Z0-9_]*=', ocurrencia))
# Se le quita el "float", si está sólo al principio de la subcadena, y los símbolos para que quede el nombre de la variable
vars_floats_dec = [re.sub(r'^float|[\W_]+', '', elemento) for elemento in vars_floats_dec_aux]
vars_floats_ini = [re.sub(r'^float|[\W_]+', '', elemento) for elemento in vars_floats_ini_aux]
# Se quitan las 'f' que se utilizan para inicializar un float "float decimal5 = 10.0f;" porque pasan la función regex
# Si las 'f' declaradas son mayor o igual a las inicializadas se quitan el número de inicializadas, por si hay una variable llamada 'f'
i = 0
j = 0
if vars_floats_dec.count('f') >= len(vars_floats_ini):
    for cadena in vars_floats_dec:
        if 'f' in cadena and j < len(vars_floats_ini):
            vars_floats_dec[i] = cadena.replace('f', '')
            j += 1
        i += 1
vars_floats_dec = [cadena for cadena in vars_floats_dec if cadena]   

#-----------------------------------------------------FLOAT_ARREGLO-----------------------------------------------------------

# Se buscan todas las subcadenas que cumplan con la expresion regular encontrada para detectar las siguientes cadenas:
# float[] arregloDecimal1;
# float[] arregloDecimal2, arregloDecimal3, arregloDecimal4;
# float[] arregloDecimal5 = new float [3];
# float[] arregloDecimal6 = new float[4], arregloDecimal7 = new float[5];
# float[] arregloDecimal8 = {1.1f, 1.1f, 1.1f, 1.1f, 1.1f, 1.1f, 1.1f};
# float[] arregloDecimal9 = {1.1f, 2.1f, 3.1f, 4.1f, 5.1f}, arregloDecimal10 = {6.1f, 7.1f, 8.1f, 9.1f, 10.1f};
ocurrencias_floats_array = re.findall(r'float\[\][a-zA-Z][a-zA-Z0-9_]*(?:=newfloat\[\d+\])?(?:,[a-zA-Z][a-zA-Z0-9_]*(?:=newfloat\[\d+\])*)*;', nuevo_contenido)
# Se agrega una nueva función regex para encontrar los casos en donde se inicializa la variable de la siguiente manera "float[] arregloDecimal8 = {1.1f, 1.1f, 1.1f, 1.1f, 1.1f, 1.1f, 1.1f};"
ocurrencias_floats_array_aux = re.findall(r'float\[\][a-zA-Z][a-zA-Z0-9_]*=\{-?\d+\.\d+f(?:,-?\d+\.\d+f)*\}(?:,[a-zA-Z][a-zA-Z0-9_]*=\{-?\d+\.\d+f(?:,-?\d+\.\d+f)*\})*;', nuevo_contenido)
# Se extiende el arreglo para agregar los casos encontrados en la segunda función regex
ocurrencias_floats_array.extend(ocurrencias_floats_array_aux)
# Se cuentan las variables declaradas del arreglo obtenido con las coincidencias que encontró la función regex
# Las cuenta encontrando '{' dentro de la subcadena, si es que hay y, en el caso de que no haya, cuenta ',' + 1 
floats_array_declarados = 0
for ocurrencia in ocurrencias_floats_array:
    if '{' in ocurrencia:
        floats_array_declarados += ocurrencia.count('{')
    elif ',' in ocurrencia:
        floats_array_declarados += ocurrencia.count(',') + 1
    else:
        floats_array_declarados += 1
# Se cuentan las variables inicializadas del arreglo obtenido con las coincidencias que encontró la función regex
# Las cuenta encontrando '{' y '[', pero en el caso '[' se resta 1 para no contar el de la declaración inicial "float[]"       
floats_array_inicializados = 0
for ocurrencia in ocurrencias_floats_array:
    if '[' in ocurrencia and ocurrencia.count('[')>1 or '{' in ocurrencia:
        floats_array_inicializados += ocurrencia.count('[') -1
        floats_array_inicializados += ocurrencia.count('{')
# Se guarda el nombre de las variables en dos grupos, declaradas e inicializadas
vars_floats_array_ini = []
vars_floats_array_dec = []
vars_floats_dec_array_aux = []
vars_floats_ini_array_aux = []
for ocurrencia in ocurrencias_floats_array:
    vars_floats_dec_array_aux.extend(re.findall(r'float\[\][a-zA-Z][a-zA-Z0-9_]*,|[a-zA-Z][a-zA-Z0-9_]*;|[a-zA-Z][a-zA-Z0-9_]*,|float\[\][a-zA-Z][a-zA-Z0-9_]*;', ocurrencia))
    vars_floats_ini_array_aux.extend(re.findall(r'float\[\][a-zA-Z][a-zA-Z0-9_]*=|,[a-zA-Z][a-zA-Z0-9_]*=', ocurrencia))
# Se le quita el "float[]", si está sólo al principio de la subcadena, y los símbolos para que quede el nombre de la variable
vars_floats_array_dec = [re.sub(r'^float|[\W_]+', '', elemento) for elemento in vars_floats_dec_array_aux]
vars_floats_array_ini = [re.sub(r'^float|[\W_]+', '', elemento) for elemento in vars_floats_ini_array_aux]
# Si el número de todas las variables menos las inicializadas es menor que las variables no inicializadas que se encontraron después (vars_floats_array_dec) 
# se quitan el número de 'f' de la diferencia entre las variables encontradas y la resta de todas las variables mesnos las inicializadas, 
# por si hay una variable que termine con 'f' 
nfloats_array_no_declarados = floats_array_declarados - floats_array_inicializados 
i = 0
j = 0
para = len(vars_floats_array_dec)-nfloats_array_no_declarados
if vars_floats_array_dec.count('f') >= len(vars_floats_array_ini):
    for cadena in vars_floats_array_dec:
        if 'f' in cadena and j < para:
            vars_floats_array_dec[i] = cadena.replace('f', '')
            j += 1
        i += 1
vars_floats_array_dec = [cadena for cadena in vars_floats_array_dec if cadena] 

################################################### PRINTS ###################################################

print("--------------------------------------")

print("Número total de variables declaradas = ", ints_declarados + ints_array_declarados + strings_declarados + strings_array_declarados + floats_declarados + floats_array_declarados)
print("Número total de variables inicializadas = ", ints_inicializados + ints_array_inicializados + strings_inicializados + strings_array_inicializados + floats_inicializados + floats_array_inicializados)

print("Número total de variables declaradas inicializadas array = ", ints_array_inicializados + strings_array_inicializados + floats_array_inicializados)
print("Número total de variables declaradas no inicializadas array = ", (ints_array_declarados-ints_array_inicializados) + (strings_array_declarados-strings_array_inicializados) + (floats_array_declarados-floats_array_inicializados))
print("Número total de variables declaradas inicializadas no array = ", ints_inicializados + strings_inicializados + floats_inicializados)
print("Número total de variables declaradas no inicializadas no array = ", (ints_declarados-ints_inicializados) + (strings_declarados-strings_inicializados) + (floats_declarados-floats_inicializados))

print("Número total de variables de tipo INT = ", ints_declarados + ints_array_declarados)
print("Número total de variables de tipo STRING = ", strings_declarados + strings_array_declarados)
print("Número total de variables de tipo FLOAT = ", floats_declarados + floats_array_declarados)

print("Número total de variables de tipo arreglo = ", ints_array_declarados + strings_array_declarados + floats_array_declarados)

print("Número total de variables declaradas con valor constante = ", len(re.findall(r'final(int|String|float)', nuevo_contenido)))


arreglofin = []
arreglofin.append("-----------NO INICIALIZADAS-----------")
arreglofin.extend(vars_ints_dec)
arreglofin.extend(vars_ints_array_dec)
arreglofin.extend(vars_strings_dec)
arreglofin.extend(vars_strings_array_dec)
arreglofin.extend(vars_floats_dec)
arreglofin.extend(vars_floats_array_dec)
arreglofin.append("-----------INICIALIZADAS--------------")
arreglofin.extend(vars_ints_ini)
arreglofin.extend(vars_ints_array_ini)
arreglofin.extend(vars_strings_ini)
arreglofin.extend(vars_strings_array_ini)
arreglofin.extend(vars_floats_ini)
arreglofin.extend(vars_floats_array_ini)

for fila in arreglofin:
    print(fila)
