# Ficheros A y ficheros B agregando un archivo Fusion
## Funcionamiento y planteamiento
el programa debe crear o leer  unos archivos conocidos como archivos A y B para almacenar unos registros de unos productos para implementarlos en un excel a forma de produccion, el programa en si esta en fase beta debido a tiempo/desarrollo 

### Funcion Principal Main()
```c++
int main(int argc, char const *argv[])
{
    string fichero_A,fichero_B;
    fichero_A = "fichero_A.txt";
    fichero_B = "fichero_B.txt";
    cout<<"bienvenido a mi programa fichero_AB suponemos manjear 2 sucursales"<<endl;
    while(true){
        system("cls");
        string seleccion;
        cout<<"eliga una opcion"<<endl;
        cout<<"1.insertar datos en fichero_A"<<endl;
        cout<<"2.insertar datos en el fichero_B"<<endl;
        cout<<"3.visualizar datos del fichero_A"<<endl;
        cout<<"4.visualizar datos del fichero_B"<<endl;
        cout<<"5.archivo fusion "<<endl;
        cout<<"6. salir"<<endl;
        getline(cin,seleccion);
        if (seleccion=="1"){
            insercion(fichero_A);
        }
        if (seleccion=="2"){
            insercion(fichero_B);
        }
        if (seleccion=="3"){
            revision(fichero_A);
            getch();
        }
        if (seleccion=="4"){
            revision(fichero_B);
            getch();
        }
        if (seleccion=="5")
        {
            fusion(fichero_A,fichero_B);
            getch();
        }
        if (seleccion=="6")
        {
            break;
        }
        
    }
    return 0;
}
```
es una estructura de seleccion del programa que permite interactuar para que el usario pueda usarlo
## funciones principales del programa 
### Recoleccion de datos
```c++
void revision(string fichero){
    int control_estado = 0;
    int conteo= 0;
    ifstream archivo;
    string obtener_linea;
    string copia;
    archivo.open(fichero,ios::in);
    while (!archivo.eof()){
        getline(archivo,obtener_linea);
        copia +=obtener_linea;
        if (copia.length()==0)
        {
            cout<<"archivo vacio";
            break;
        }
        
        copia +=' ';
    }
    for (size_t i = 0; i < copia.length(); i++){
        if (copia[i] == ' '){
            conteo++;
        }    
    }
    int espacios[conteo];
    for (size_t i = 0; i < copia.length(); i++){
        if (copia[i] == ' '){
            espacios[control_estado] = i;
            control_estado++;
        }      
    }
    control_estado = 0;
    string palabras[conteo];
    int i = 0;
    while (aceptado(i,conteo)){
      if (control_estado == 0){
        palabras[i] = primerelemento(espacios[control_estado],copia);
        i++;
      }
      palabras[i] = seleccion(espacios[control_estado],espacios[i],copia);
      i++;
      control_estado++;
    }
    int estado=0;
    int objetos = conteo/3;
    medicamento prueba[objetos];
    for (size_t i = 0; i < objetos; i++){
        prueba[i].nombre = palabras[estado];
        estado++;
        prueba[i].codigo = palabras[estado];
        estado++;
        prueba[i].stock = convertir_entero(palabras[estado]);
        estado++;
    }
    for (size_t i = 0; i < objetos; i++){
        cout<<prueba[i].nombre<<" "<<prueba[i].codigo<<" "<<prueba[i].stock<<endl;
    }
}
```
esta funcion permite visualizar los datos que empieza obteniendo los datos del txt y guardandolos como un string que contiene dicha informacion la cual esta misma info se recolecta y se administran los espacios totales a partir de ellos se recolectan los las palabras guardarlas en un objeto y mostrarlas, de esta funcion parte la idea de la ideologia de las otras tomando los datos correctos de esta misma y almacenarlos en la funcion de solicitadada 
### Funciones de Recoleccion
#### funcion de obtener cuantos registros de estan en el archivo
```c++
int longitud(string fichero){
    int control_estado = 0;
    int conteo= 0;
    ifstream archivo;
    string obtener_linea;
    string copia;
    archivo.open(fichero,ios::in);
    while (!archivo.eof()){
        getline(archivo,obtener_linea);
        copia +=obtener_linea;
        if (copia.length()==0)
        {
            cout<<"archivo vacio";
            break;
        }
        copia +=' ';
    }
    for (size_t i = 0; i < copia.length(); i++){
        if (copia[i] == ' '){
            conteo++;
        }    
    }
    int objetos = conteo/3;
    return objetos;
}
```
#### Recoleccion de registros del txt 
```c++
medicamento registro(string fichero,int iterante){
    int control_estado = 0;
    int conteo= 0;
    ifstream archivo;
    string obtener_linea;
    string copia;
    archivo.open(fichero,ios::in);
    while (!archivo.eof()){
        getline(archivo,obtener_linea);
        copia +=obtener_linea;
        if (copia.length()==0)
        {
            cout<<"archivo vacio";
            break;
        }
        
        copia +=' ';
    }
    for (size_t i = 0; i < copia.length(); i++){
        if (copia[i] == ' '){
            conteo++;
        }    
    }
    int espacios[conteo];
    for (size_t i = 0; i < copia.length(); i++){
        if (copia[i] == ' '){
            espacios[control_estado] = i;
            control_estado++;
        }      
    }
    control_estado = 0;
    string palabras[conteo];
    int i = 0;
    while (aceptado(i,conteo)){
      if (control_estado == 0){
        palabras[i] = primerelemento(espacios[control_estado],copia);
        i++;
      }
      palabras[i] = seleccion(espacios[control_estado],espacios[i],copia);
      i++;
      control_estado++;
    }
    int estado=0;
    int objetos = conteo/3;
    medicamento prueba[objetos];
    for (size_t i = 0; i < objetos; i++){
        prueba[i].nombre = palabras[estado];
        estado++;
        prueba[i].codigo = palabras[estado];
        estado++;
        prueba[i].stock = convertir_entero(palabras[estado]);
        estado++;
    }
    return prueba[iterante];
}
```
### la funcion de aplicacion
```c++
bool aplicacion(medicamento iterante[],medicamento elemento){
    
    for (size_t i = 0; iterante[i].stock != 0; i++)
    {
        if (elemento.codigo==iterante[i].codigo)
        {
            return false;
        }
        
    }
    return true;
}
```
la funcion aplicacion forma parte de la funcion fusion tiene un recorrido controlado de un arreglo formado de una idea que si el elemento recorrido de un arreglo en constante movimiento a nivel de construccion a partir de otro arreglo. si el elemento que esta en el arreglo en constante a base del arreglo anterior ya esta y vuelve a pasar otra vez retornara false de lo contrario si el elemento no esta retornara true.
# La funcion fusion
principalmente era necesario documentar las anteriores funciones para ver su naturealeza por partes ya que la funcion que realize el trabajo mas complejo a nivel logico es la funcion conocida como fusion 
```c++
void fusion(string fichero_1,string fichero_2){
    ofstream archivo;
    archivo.open("final.txt",ios::out);
    archivo<<"";
    medicamento fichero_A[longitud(fichero_1)];
    medicamento fichero_B[longitud(fichero_2)];
    for (size_t i = 0; i < longitud(fichero_1); i++){
        fichero_A[i] = registro(fichero_1,i);
    }
    for (size_t i = 0; i < longitud(fichero_2); i++){
        fichero_B[i] = registro(fichero_2,i);
    }
    medicamento fichero_final[longitud(fichero_1)+longitud(fichero_2)];
    for (size_t i = 0; i < longitud(fichero_1); i++)
    {
        fichero_final[i]= fichero_A[i];
    }
    int control = 0;
    for (size_t i = longitud(fichero_1); i < longitud(fichero_1)+longitud(fichero_2); i++)
    {
        fichero_final[i] = fichero_B[control];
        control++;
    }
    int tupla_control = 0;
    medicamento tupla[longitud(fichero_1)+longitud(fichero_2)];
    for (size_t i = 0; i < longitud(fichero_1)+longitud(fichero_2); i++)
    {
        if (true==aplicacion(tupla,fichero_final[i]))
        {
            tupla[tupla_control] = fichero_final[i];
            tupla_control++;
        }
    }
    medicamento inventario[tupla_control];
    for (size_t i = 0; i < tupla_control; i++){
        inventario[i] = tupla[i];
    }
    for (size_t i = 0; i < tupla_control; i++)
    {
        reporte(inventario[i],fichero_final,longitud(fichero_1)+longitud(fichero_2));
    }
    medicamento tupla_ordenada[tupla_control];
    for (size_t i = 0; i < tupla_control; i++)
    {
        tupla_ordenada[i] = registro("final.txt",i);
    }
}
```
en esta analogia de tupla se utiliza la recursion llamando a un arreglo dinamico de elementos no fijo y llenarlo hasta que este cumpla el registro unico de cada uno de ellos e introducirlos en txt y almacenarlos para mas tarde.
## Elementos de Validacion
### conversion de enteros
```c++
int convertir_entero(string cadena){
    int total = 0;
    float numero[cadena.length()];
    for (size_t i = 0; i < cadena.length(); i++)
    {
        numero[i] = (cadena[i]-'0');
        numero[i] = numero[i]/10;
    }
    for (int i = 0; i < cadena.length(); i++)
    {
        for (size_t j = 0; j < (cadena.length()-i);j++)
        {
            numero[i] = numero[i]*10;
        }
        total+= numero[i];
    }
    return total;
    
}
```

esta funcion toma de parametro una cadena de string que solamente contenga numeros enteros previamente validados de la funcion (askii_num) de no ser asi, esta funcion tiene defectos para calcular del string propuesto a la transformacion numerica, para empezar se calcula la longitud de la cadena que como un dato numerico para es decir si el elemento tiene 4 al sacarlo del .lenght() el arreglo numero tendra de espacios a ocupar 4, se itera cada elemento del string y se usa la conversion askii de -'0' para guardar del el string como un entero ya que el arreglo numero esta lleno, se procede a crear otras variable para acumular los resultados por cada iteracion descompuesta tal que dando un ejemplo

```
5342 ramificado
5
4
3
2
pero su longitud de string antes de convertirlos a un arreglo de numeros me indica su unidades y me quedaria
5*1000
3*100
4*10
2*1
---5432----
```

### Validacion askii

```c++
string askii(string enunciado){
    while (true)
    {
        string nombre;
        cout<<enunciado;
        getline(cin,nombre);
        if (nombre.length()==0)
        {
            cout<<"no compatible "<<endl;
        }
    
        int conteo = 0;
        int askiinombre[nombre.length()];
        for (size_t i = 0; i < nombre.length(); i++){
            if (nombre[i] == ' '){

                nombre[i] = '_';
            }
        
            askiinombre[i] = nombre[i] - '0';
        }
        for (size_t i = 0; i < nombre.length(); i++){
            conteo += verificar(askiinombre[i]);
        }
        if (conteo==nombre.length())
        {
            return nombre;
        }else{
            cout<<"no compatible"<<endl;
        }
    }
}
```
esta funcion validador de nivel bajo en cuestion de redimiento para que solo los elementos que cumplan las condiciones adecuadas de la funcion verificar() para que vuelva a preguntar los datos ya que estra conformado de un while true cumpliendo que cuando se haga la verficacion completa retorne el resultado.
## askii_verifiacion
```c++
int verificar(int x){
    char abecedario[] = {'a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z','_'};
    for (size_t i = 0; i < 27; i++)
    {
        if (x==(abecedario[i] - '0'))
        {
            return 1;
        }
        
    }
    return 0;
}
```
una funcion que este forma parte de askii para identificar que esta para identificae los caracteres validos en su codigo askii y retornar si pertence con 1 o no retornando 0
## Variaciones de askii numericas

### askii_numerico
```c++
string askii_num(string enunciado){
    while (true)
    {
        string nombre;
        cout<<enunciado;
        getline(cin,nombre);
        if (nombre.length()==0)
        {
            cout<<"no compatible "<<endl;
        }
        
        int conteo = 0;
        int askiinombre[nombre.length()];
        for (size_t i = 0; i < nombre.length(); i++){
            if (nombre[i] == ' '){

                nombre[i] = '_';
            }
        
            askiinombre[i] = nombre[i] - '0';
        }
        for (size_t i = 0; i < nombre.length(); i++){
            conteo += verificar_num(askiinombre[i]);
        }
        if (conteo==nombre.length())
        {
            return nombre;
        }else{
            cout<<"no compatible"<<endl;
        }
    }
}
```
### verificacion_num
```c++
int verificar_num(int x){
    char abecedario[] = {'0','1','2','3','4','5','6','7','8','9'};
    for (size_t i = 0; i < 10; i++)
    {
        if (x==(abecedario[i] - '0'))
        {
            return 1;
        }
        
    }
    return 0;
}
```
