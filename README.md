## **Estándares de código y TypeScript**

- Nombres descriptivos para variables, funciones.
    
    ```tsx
    const PORT = 4000;
    const connectDB = () => {
       //...código
    }
    ```
    
- Las variables y funciones nombradas en camelCase.
    
    ```tsx
    const variablenocamelcase = "Mal"
    const variableSiCamelCase = "Bien"
    
    ```
    
- Las constantes en mayúsculas con guiones bajos como espacios.
    
    ```tsx
    const PORT = 4000
    const myConstants = {
    	NAME_AND_SURNAME:"Camila Pérez",
    	AGE: 24,
    	...
    }
    ```
    
- Una indentación consistente, espacios entre operadores para una buena legibilidad y espacios entre comas y puntos y coma.
    
    ```tsx
    // Identación consistente: Yo propongo 3 espacios en blanco.
    
    // Espacios entre operadores: (ej)
    const string3 = "3";
    const int3 = 3;
    int3 == string3;
    
    // Espacios entre comas y puntos y coma: (ej)
    const Componente = ({arr, obj, ...rest}) => {
    	for(const i = 0; i < arr.legth; i++){
    		//...code	
    	}
    
    ```
    
- Comentarios descriptivos para explicar el propósito del código.
- Comentar cualquier código que sea confuso o requiera una explicación adicional.
- Evitar comentarios redundantes que no agreguen valor al código.
- Siempre utiliza el punto y coma al final de cada sentencia. (Yo prefiero evitarlos)
- Utilizar llaves ({}) para delimitar bloques de código, incluso si solo constan de una línea.
    
    ```tsx
    // Aunque es más legible el primer método, el estándar sugiere utilizar el segundo.
    
    if (true) return "Mal"
    
    if (true) {
    	return "Perfecto"
    }
    ```
    
## Usar Linter
 - El linter nos permite definir una serie de reglas las cuales todo el equipo debe de seguir para tener un código mas limpio.
   por ejemplo, cuantas identaciones hay que hacer, si usar punto y como, si usar comillas simples o dobles, etc.
   nosotros podemos configurar que reglas seguir o usar un conjunto de reglas ya definidas, como por ejemplo `standard`.
## Estándares para TailwindCSS

- **Organización de clases**.
    - Utilizar utilidades de TailwindCSS en lugar de crear nuevas clases personalizadas siempre que sea posible.
    - Evitar la duplicación innecesaria de clases o superposición de clases.
        
        ```html
        <-- En este caso, flex se superpone con block. -->
        <button class="flex flex-col block">
        	Click me!
        </button>
        ```
        
- **Responsividad**
    - Establecer en el config de TailwindCSS un estándar de responsividad
        
        ```json
        "md": "680px",
        "lg": "1024px",
        "xl": "1240px",
        "etc": "..."
        ```
        
    - Utilizar el estándar de responsividad propuesto en nuestros componentes.
    - Agrupar las clases responsivas para evitar la repetición y mejorar la legibilidad.
    
    ```html
    <div class="flex flex-col w-40 md:w-44 lg:w-48 lg:flew-row xl:w-56">
    	<button>Botón 1</button>
    	<button>Botón 2</button>
    	<button>Botón 3</button>
    </div>
    ```
    
- **Personalización**
    - Utilizar las capacidades de personalización de TailwindCSS para ajustar los colores, fuentes y otras configuraciones.
    - Definir clases personalizadas en tu archivo de configuración de TailwindCSS en lugar de escribir estilos personalizados adicionales.
