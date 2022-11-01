# Informe Técnico

## Informe Técnico de trabajo sobre Goffice

### Función `setTerms`

Se crea la función `setTerms` y su sintaxis es la siguiente:

```php
private function setTerms(int $id, array $data): void
```

Uso de este método:

```php
$this->setTerms($id, $data)
```

Donde `$id` es el identificador de la cotización que se creará y `$data`, todos los campos del formulario.

### Función `getTerms`

Se crea la función `getTerms` para obtener todos los campos con sus valores de los términos y condiciones.

Sintaxis:

```php
private function getTerms(int $id = NULL): object
```

Donde `$id` es el identificador de los términos y condiciones. Si no se establece el `id` o no se encuentran los términos y condiciones en la base de datos se toman las que se encuentran definida por defecto.

Uso de la función:

```php
$data = $this->getTerms();
```

### Función `compile`

La función `compile` se utiliza para formatear texto plano a partir de ciertos patrones. Útil para permitir identificar los párrafos, saltos de líneas, las negritas, cursivas o negritas cursivas, así como también las viñetas.

Sintaxis:

```php
private function compile(string $text): string
```

Donde `$text` es el texto que se pasará como argumento de la función para ser formateado.

**Uso de la función:**

```php
$text = $this->compile($text);
```

### Función `convertParagraphToItems`

La función `convertParagraphToItems` convierten los párrafos HTML a listas desordanadas o viñetas si detecta guiones (-) dentro de él.

**Sintaxis:**

```php
private function convertParagraphToItems(string $html): string
```

**Uso de la función:**

```php
$html = convertParagraphToItems($html);
```

### Función `replace`

La función `replace`, como su nombre lo indica, sirve para reemplazar. Si bien, existe una función de forma nativa en PHP denominada `preg_replace`, el objeto de la misma es que se pase en él como tercer argumento una función.

La idea es hacer reemplazos de forma quirúrgicas.

**Sintaxis:**

```php
private function replace(string $pattern, string $text, callable $fn): string
```

Donde `$pattern` es la expresión que se pasa como primer argumento, `$text` el texto que se tomará para realizar el reemplazo y `$fn` la función que se pasará como argumento y que además, cuenta con un parámetro que es una cadena de texto, es decir, el texto encontrado.

**Uso de la función:**

```php
$string = $this->replace($pattern, $text, function(string $string) {
    return "<strong>$string</strong>";
});
```

Lo anterior no es una única forma de reemplazo, es una de las tantas que se pueden utilizar.

### Función `filterMT`

Esta funciòn permite filterar los métodos y técnica analítica seleccionada por el usuario. Cuenta con dos argumentos.

**Sintaxis:**

```php
private function filterMT(array $array, array $identifiers): array
```

**`array $array`:** Es el array de métodos o técnica analítica que debe pasarse como primer argumento de la función. La idea es filtrar a partir de los identificadores los datos seleccionados por el usuario.

**`array $identifiers`:** Debe pasar un array de identificadores numéricos como segundo argumento para devolver lo que el usuario eligió.

### Función `getMT`

La función `getMT` nos permite obtener una colección de métodos y técnica analítica general.

**Sintaxis:**

```php
private function getMT(): Collection
```

**Uso de la función:**

```php
$method_and_technicals = $this->getMT();
```

### Función getDataQuotations

Esta función es utiliza por `getTerms` para obtener los términos y condiciones a partir de las cotizaciones que genere el usuario.

**Sintaxis:**

```php
private function getDataQuotations(int $id = NULL): object
```

Donde `$id` es el identificador de la cotización generada por el usuario, pero es opcional si desea tomar los términos y condiciones por defecto.

**Uso de la función:**

```php
$data = $this->getDataQuotations();
```

### Función `returnRegister`

Este método o función se utiliza para validar los datos que se obtienen de métodos y ténica analítica desde la vista `proposal-pdf.blade.php`.

**Sintaxis:**

```php
public function returnRegister(array $array, int $key): object
```

**Uso de la función:**

```blade
{{ $proposalController->returnRegister($terms->methods, $key)->value ?? '-' }}
```

### Documento PDF generado automáticamente

La cotización convertida en un **documento PDF** y que además contienen los términos y condiciones obtienen sus datos a partir de los que almacenados en la tabla `new_proposals_term`. Sin embargo, no se toman todos los items o campos de la base de datos, pese a guardarse en ella, porque de lo contario, se dañaría el formato del documento de doble columna.

Si no existen datos en `new_proposals_term` se tomarán los datos por defecto que se encuentran almacenados en la tabla `new_proposals_term_preview`.
También se implementan los **Métodos y Técnica Analítica**.

### Creación de la cotización

Todos los nuevos campos que se han creado para almacenar los términos y condiciones se almacenan sin excepción en la base de datos. Específicamente, en la tabla `new_proposals_term`.

### Creación del script de actualización

Se crea un script denominado `update` con el objeto que todas las actualizaciones que se lleven al hosting sean innecesaria la autenticación manual. El archivo lo hará por la persona de forma automática.

### Análisis y depuración

Se analiza y optimiza el código para generar menos basura. De acuerdo al análisis se harán otras optimizaciones para mañana.

Depura el código para generar menos basura. Se agrega la siguiente función al controlador:

```php
/**
     * Set the background image in the PDF document.
     *
     * @return string
     */
    public function setImagePDF(): string {
        $img = './user-uploads/temp/template.jpg';
        $base64 = '';

        if (file_exists($img)) {
            $base64 = base64_encode(file_get_contents($img));
        }

        if (!empty($base64)) {
            return "<img class=\"templage__img\" src=\"data:image/jpeg;base64,$base64\" alt=\"Background\" />";
        }

        return '';
    }

```
