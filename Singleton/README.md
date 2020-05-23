# Singleton
El patron Singleton se asegura de que una clase determinada tenga una sola instancia, y provee un punto global para acceder a esta. Este patron se logra declarando como privado el constructor de la clase y creando un metodo que crea una instancia del objeto si es que no existe.

![SingletonUML](Singleton.png)

## Ejemplo
Supongamos que tenemos un juego de un solo jugador en el que el que este debe usar el teclado para mover al personaje. Para mapear el teclado con los movimientos del personaje, existe una clase llamada Teclado:
```java
    public class Teclado{
        public Teclado(){ //constructor
            mapearTeclado();
        } 
        private mapearTeclado(){...}
    }
```
Aca tenemos un claro problema, y es que nada impediria que se pueda hacer lo siguiente:
```java
    public class Juego(){
        Teclado t1 = new Teclado();
        Teclado t2 = new Teclado();
    }
```
Esto ocasionaria que existan dos teclados para el mismo juego, cosa ilogica ya que el juego es para un solo jugador. Para solucionar este problema se puede utilizar el patron Singleton
![TecladoUML](Teclado.png)

Quedando la clase Teclado de la siguiente manera:
```java
    public class Teclado{
        private Teclado miTeclado;
        private Teclado(){ //constructor privado
            mapearTeclado();
        } 
        private mapearTeclado(){...}
        
        public static Teclado getTeclado(){
            if(this.miTeclado == null){
                this.miTeclado = new Teclado();
            }
            return this.miTeclado
        }
    }
```
Para obtener una instancia de teclado:
```java
    public class Juego(){
        Teclado t1 = Teclado.getTeclado();
        Teclado t2 = Teclado.getTeclado(); 
        //t1 y t2 son la misma instancia (mismo puntero)
    }
```
De esta manera logramos que solo exista una instancia de Teclado.
