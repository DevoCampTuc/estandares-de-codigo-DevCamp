## **Estándares de código y TypeScript**

-  Nombres descriptivos para variables, funciones.
   ```tsx
   const PORT = 4000;
   const connectDB = () => {
   	//...código
   };
   ```
-  Las variables y funciones nombradas en camelCase.
   ```tsx
   const variablenocamelcase = 'Mal';
   const variableSiCamelCase = 'Bien';
   ```
-  Las constantes en mayúsculas con guiones bajos como espacios.
   ```tsx
   const PORT = 4000
   const myConstants = {
   	NAME_AND_SURNAME:"Camila Pérez",
   	AGE: 24,
   	...
   }
   ```
-  Una indentación consistente, espacios entre operadores para una buena legibilidad y espacios entre comas y puntos y coma.

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

-  Comentarios descriptivos para explicar el propósito del código.
-  Comentar cualquier código que sea confuso o requiera una explicación adicional.
-  Evitar comentarios redundantes que no agreguen valor al código.
-  Siempre utiliza el punto y coma al final de cada sentencia. (Yo prefiero evitarlos)
-  Utilizar llaves ({}) para delimitar bloques de código, incluso si solo constan de una línea.

   ```tsx
   // Aunque es más legible el primer método, el estándar sugiere utilizar el segundo.

   if (true) return 'Mal';

   if (true) {
   	return 'Perfecto';
   }
   ```

## **Formateo de código PRETTIER**

Prettier (extensión de VS) es una herramienta de formateo de código que se utiliza para mantener la consistencia en el estilo de escritura del código en un proyecto. Automáticamente ajusta y reorganiza el código fuente según un conjunto de reglas predefinidas, lo que ayuda a garantizar una apariencia uniforme en todo el código y facilita la lectura y comprensión del mismo.

```tsx
   // Settings a utilizar.
   // copiar en "Manage > Settings > Open Settings (JSON)"
    "editor.wordWrap": "on",
	"editor.defaultFormatter": "esbenp.prettier-vscode",
	"editor.formatOnSave": true,
	"prettier.singleQuote": true,
	"prettier.jsxSingleQuote": true,
	"prettier.tabWidth": 3,
	"prettier.trailingComma": "all",
	"prettier.useTabs": true,
```

## Usar Linter

-  El linter nos permite definir una serie de reglas las cuales todo el equipo debe de seguir para tener un código mas limpio.
   por ejemplo, cuantas identaciones hay que hacer, si usar punto y como, si usar comillas simples o dobles, etc.
   nosotros podemos configurar que reglas seguir o usar un conjunto de reglas ya definidas, como por ejemplo `standard`.

## Estándares para TailwindCSS

-  **Organización de clases**.
   -  Utilizar utilidades de TailwindCSS en lugar de crear nuevas clases personalizadas siempre que sea posible.
   -  Evitar la duplicación innecesaria de clases o superposición de clases.
      ```html
      <-- En este caso, flex se superpone con block. -->
      <button class="flex flex-col block">Click me!</button>
      ```
-  **Responsividad**
   -  Establecer en el config de TailwindCSS un estándar de responsividad
      ```json
      "md": "680px",
      "lg": "1024px",
      "xl": "1240px",
      "etc": "..."
      ```
   -  Utilizar el estándar de responsividad propuesto en nuestros componentes.
   -  Agrupar las clases responsivas para evitar la repetición y mejorar la legibilidad.
   ```html
   <div class="flex flex-col w-40 md:w-44 lg:w-48 lg:flew-row xl:w-56">
   	<button>Botón 1</button>
   	<button>Botón 2</button>
   	<button>Botón 3</button>
   </div>
   ```
-  **Personalización**
   -  Utilizar las capacidades de personalización de TailwindCSS para ajustar los colores, fuentes y otras configuraciones.
   -  Definir clases personalizadas en tu archivo de configuración de TailwindCSS en lugar de escribir estilos personalizados adicionales.

## **Carpetas y rutas**

-  **Carpeta "components"**

   -  Dentro de la carpeta "src"
   -  Contiene componentes reutilizables en el proyecto.
   -  En caso de que un componente requiera o se complemente con otro archivo, estos deben estár dentro de una carpeta del mismo nombre del componente. (Ej: una carpeta con el nombre del componente donde contenga el archivo .tsx y el .css que le corresponda)

-  **Carpeta "hooks"**

   -  Dentro de la carpeta "src"
   -  Contiene los archivos de los custom hooks.
   -  Cada archivo debe tener un nombre específico a la función que cumpla.

# Estándar de pruebas

## 1. **Configuración:**

1.1  **Directorios:**

```tsx
/cypress
	/fixtures: Almacena archivos de datos de prueba.
	/integration: Contiene archivos de pruebas.
	/pages: Alberga las clases de páginas (page objects) que representan elementos y acciones en el sitio.
	/support: Incluye archivos de soporte como comandos personalizados, funciones auxiliares y configuraciones.
```

1.2  **Convenciones de nomenclatura:**

- Nombre de archivo de prueba: **`nombreDePrueba.cy.js`**
- Nombre de prueba: **`should realizar alguna accion`**
- Nombre de página (page object): **`NombreDePagina`**
- Nombres y comentarios en inglés (evitemos el Espanglish) 🙏🏻.

1.3  **Configuración común y opciones estándar:**

- Establecer la URL base en `cypress.json` . Ejemplo: `"baseUrl":"http://example.com"`
- Configurar un tiempo de espera global en **`cypress.json` `"defaultCommandTimeout": 5000`**.

1.4  **Manejo adecuado de datos de prueba:**

- Crear un archivo JSON llamado **`datos_prueba.json`** en la carpeta **`fixtures`** con los datos de prueba necesarios y utilizarlo en tus pruebas con **`cy.fixture()`**.

## 2. **Buenas prácticas:**

1. Utilizar **`should`** para realizar aserciones en Cypress, por ejemplo: **`cy.get('#elemento').should('be.visible')`**.

2.1  **Selectores:** Siempre debemos usar para pruebas con cypress en el html atributos de tipo data, en este caso estos deben estar definidos de así: `data-cy=””`

Ejemplo:
`<button data-cy="submit">Submit</button> javascript cy.get('[data-cy=submit]').click()` Esta opción asegura que siempre se tendrá el mismo objeto.

2.2  Usar `cy.contains()` solo si queremos que falle la prueba en caso de que cambie el elemento. Depender mucho de este selector basado en texto hace que el test se vuelva frágil. Por ejemplo, 1. Si hay más de un elemento con el mismo texto puede devolver el elemento incorrecto y volverlo propenso a errores. 2. Cualquier camio en el texto de la página puede romper los test incluso si la funcionalidad es la misma.

2.3  ************************************Sitios externos:************************************ Evitar en lo posible interactuar en sitios o servidores en los que no tenemos control. Si es inevitable, usar `cy.visits()` , pero tener en cuenta que puede bloquear los testing.

2.4  **Logging**: Usar Stub para hacer creer a la aplicación que hicimos un logging exitoso o usar `cy.request()`

2.5  **Separa la UI de la funcionalidad.** En la practica, extrae los datos que necesites de una manera abstracta sin que este acoplada a la interfaz grafica (ya que los datos pueden cambiary la prueba puede fallar), haz aserciones de los datos puros (vs detalles visuales en HTML/CSS) y desactiva las animaciones que pueden hacer lenta la interfaz. Ejemplo: 

Correcto:

```tsx
test("When users-list is flagged to show only VIP, should display only VIP members", () => {
  // Ajustar
  const allUsers = [{ id: 1, name: "Yoni Goldberg", vip: false }, { id: 2, name: "John Doe", vip: true }];

  // Actuar
  const { getAllByTestId } = render(<UsersList users={allUsers} showOnlyVIP={true} />);

  // Afirmar - Extrae los datos de la UI primero
  const allRenderedUsers = getAllByTestId("user").map(uiElement => uiElement.textContent);
  const allRealVIPUsers = allUsers.filter(user => user.vip).map(user => user.name);
  expect(allRenderedUsers).toEqual(allRealVIPUsers); //compara datos con datos, aquí no hay UI
});
```

Incorrecto: 

```tsx
test("When flagging to show only VIP, should display only VIP members", () => {
  // Ajustar
  const allUsers = [{ id: 1, name: "Yoni Goldberg", vip: false }, { id: 2, name: "John Doe", vip: true }];

  // Actuar
  const { getAllByTestId } = render(<UsersList users={allUsers} showOnlyVIP={true} />);

  // Afirmar - Mezcla de UI y datos en las aserciones
  expect(getAllByTestId("user")).toEqual('[<li data-test-id="user">John Doe</li>]');
});
```

Ventajas:
1. Mantenibilidad: Si la UI de tu aplicación cambia, solo necesitarás hacer ajustes en las pruebas que interactúan directamente con los elementos de la UI, en lugar de modificar todas las pruebas que prueban la funcionalidad subyacente.
2. Reusabilidad: Al separar la funcionalidad de la UI, puedes reutilizar las pruebas en diferentes contextos. Por ejemplo, si tienes una prueba que verifica la funcionalidad de inicio de sesión, puedes utilizarla en diferentes escenarios donde la UI puede variar pero la funcionalidad de inicio de sesión sigue siendo la misma.
3. Enfoque en la funcionalidad: Tus pruebas se centran en probar la lógica y la funcionalidad subyacente de tu aplicación en lugar de los detalles de presentación de la interfaz.

2.6  **Independencia de Test.** Los test siempre deben de ser independientes y no debe importar si otro falla para que este se ejecute de manera normal.

2.7  **Reutilización de código**. Siempre debemos tratar de no duplicar código, un ejemplo es cuando cada test necesita ejecutar la misma acción al principio, sería una buena práctica poner estos pasos repetitivos en una función `beforeEach()` la cual se ejecutará antes de cada prueba. Por ejemplo, llenar campos de un formulario previo a enviarlos o manipularlos.

2.8  **Estructura tus test con 3 secciones bien separadas:** Ajustar, Actuar y Afirmar (AAA en inglés Arrange, Act & Assert). Seguir esta estructura garantiza que quien lea nuestro test no se estruje el cerebro en comprender los test:

- **Arrange:** configura el código, crea el escenario que el test pretende simular.
- **Act:** Ejecuta la unidad en test.
- **Assert:** Comprobar que el valor recibido satisface las expectativas.
    
    ```tsx
    // Código de prueba de llamada a API utilizando Jest y axios (biblioteca para realizar solicitudes HTTP)
    const axios = require('axios');
    
    // Caso de prueba utilizando Jest
    describe('Pruebas de llamada a API', () => {
      test('Debe obtener los datos correctos de la API', async () => {
        // Arrange
        const url = 'https://api.example.com/data';
        const expectedResponse = {
          id: 1,
          nombre: 'Ejemplo',
          correo: 'ejemplo@example.com',
        };
    
        // Act
        const response = await axios.get(url);
    
        // Assert
        expect(response.status).toBe(200);
        expect(response.data).toEqual(expectedResponse);
      });
    
      test('Debe manejar errores correctamente', async () => {
        // Arrange
        const url = 'https://api.example.com/data';
    
        // Act
        let error = null;
        try {
          await axios.get(url);
        } catch (e) {
          error = e;
        }
    
        // Assert
        expect(error).toBeDefined();
        expect(error.response.status).toBe(404);
      });
    });
    ```
    

2.9   **No uses “foo”, usa datos realistas.** A menudo, los bugs de producción se revelan bajo una entrada muy específica y sorprendente: cuanto más realista sea la entrada de un test, mayores serán las posibilidades de detectar bugs temprano.

2.10  **Evitar fixtures globales y seeds, añade datos por cada test:** cada test debe añadir y actuar en su propio conjunto de filas en base de datos para evitar el acoplamiento y poder explicar fácilmente el flujo del test. Así evitamos que test anteriores muten los datos que podrían dar fallos en tests siguientes.

Correcto:

```tsx
it("When updating site name, get successful confirmation", async () => {
  //el test esta añadiendo registors nuevos cada vez y actuando solo en esos registros
  const siteUnderTest = await SiteService.addSite({
    name: "siteForUpdateTest"
  });

  const updateNameResult = await SiteService.changeName(siteUnderTest, "newName");

  expect(updateNameResult).to.be(true);
});
```

Incorrecto:

```tsx
before(async () => {
  //añadiendo datos de sites y admin a nuestra base de datos. ¿Donde están los datos? fuera. En un json externo o en un modelo da migración
  await DB.AddSeedDataFromJson('seed.json');
});
it("When updating site name, get successful confirmation", async () => {
  //Se que el nombre de site "portal" existe, — lo he visto en seed.json
  const siteToUpdate = await SiteService.getSiteByName("Portal");
  const updateNameResult = await SiteService.changeName(siteToUpdate, "newName");
  expect(updateNameResult).to.be(true);
});
it("When querying by site name, get the right site", async () => {
  //Se que el nombre de site "portal" existe, — lo he visto en seed.json
  const siteToCheck = await SiteService.getSiteByName("Portal");
  expect(siteToCheck.name).to.be.equal("Portal"); //Fallo! El test anterior ha cambiado el nombre :[
});
```

2.11  **No captures errores, esperalos:** En lugar de usar `try-catch-finally`, usa aserciones de una línea (ej Jest: `expect(method).toThrow()`). También es obligatorio asegurarse que la excepción tenga una propiedad con el tipo de error.

Correcto:

```tsx
it("When no product name, it throws error 400", async () => {
  await expect(addNewProduct({}))
    .to.eventually.throw(AppError)
    .with.property("code", "InvalidInput");
});
```

Incorrecto:

```tsx
it("When no product name, it throws error 400", async () => {
  let errorWeExceptFor = null;
  try {
    const result = await addNewProduct({});
  } catch (error) {
    expect(error.code).to.equal("InvalidInput");
    errorWeExceptFor = error;
  }
  expect(errorWeExceptFor).not.to.be.null;
  //si esta aserción falla, el resultado/reporte del test solo mostrará
  //que algunos valores son null, no se mostrara que falta una excepción
});
```

2.12  **Categoriza los test en al menos 2 niveles:** crear al menos 2 bloques 'describe' antes de tus test: el primero es para el nombre de la unidad que está siendo testeada y el segundo es para un nivel adicional de categorización como el escenario o las categorías personalizadas.

Correcto:

```tsx
// Unidad que se está testeando
describe("Transfer service", () => {
  //Escenario
  describe("When no credit", () => {
    //Esperado
    test("Then the response status should decline", () => {});

    //Esperado
    test("Then it should send email to admin", () => {});
  });
});
```

Como se vería:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/000e4c62-6042-4eba-8d27-86a0f7471dc7/Untitled.png)

Incorrecto:

```tsx
describe('Transfer Service',() => {
	test("Then the response status should decline", () => {});

	test("Then it should send email", () => {});

	test("Then there should not be a new transfer record", () => {});
}
```

Como se vería:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/86001b8e-4c58-4793-88d4-98a0e34ac4ad/Untitled.png)

## 3. **Utilidad:**

3.1  El test debe fallar al menos una vez para evitar falsos positivos.

3.2  Funciones auxiliares y comandos personalizados: - *a definir -*

3.3  Usar un plugin de cypress para el linter. Ejemplo: `eslint-plugin-cypress`
