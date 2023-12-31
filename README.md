# Code challenge 🚀

Nuestro code challenge consiste en una prueba sencilla para conocerte mejor como ingeniero de software 😀.

**Nota:** No olvidar que la forma correcta de subir tu solución es creando un Fork de este repo y enviando un Pull Request.
Al final hay una breve guía para envíar tu solución.

-   [Problema](#problema)
-   [Tech Stack](#techstack)
-   [Opcional](#opcional)
-   [Envía tu solucion](#solución)

# Problema
Se quiere gestionar a los usuarios de un sistema, tu solución debe permitir
que un administrador pueda **Agregar**, **Listar**, **Editar** y **Eliminar** usuarios.

Para fines de este caso basta con persistir a los usuarios en local storage o en memoria.
La eliminación debe ser lógica, solo se debe modificar un booleano para indicar el estado
del registro (true = Activo, false = Inactivo).

**Mockup**
![Screenshot 2023-07-24 111910](https://github.com/luismeramosr/app-sveltekit-code-challenge/assets/41213455/ac0a0143-e9cb-402f-9d7b-3fce65ad2218)


**Ejemplos de usuarios**: 

```json
{
    "user_id": 1,
    "username": "SunTzu",
    "password": "123456",
    "active": true
}
```

```json
{
    "user_id": 2,
    "username": "Kaizen",
    "password": "123456",
    "active": false
}
```

# TechStack

<ol>
  <li>SvelteKit</li> 
</ol>

# Opcional


<ol>
  <li>Validación de formulario al momento de agregar / editar
usuarios. Por ejemplo: username requerido / password requerido + longitud mínima 10 caracteres.</li>
  <li>Mostrar errores personalizados (crear un componente Error con animaciones)</li>
</ol>

# Solución

**Crear un fork del repo**
      ![image](https://github.com/luismeramosr/app-sveltekit-code-challenge/assets/41213455/1ac756aa-2463-486e-8c98-e08697621462)
      ![image](https://github.com/luismeramosr/app-sveltekit-code-challenge/assets/41213455/fb485c1e-da23-40a2-9282-3ad73539aefe)

**Clonar el fork**
      ![image](https://github.com/luismeramosr/app-sveltekit-code-challenge/assets/41213455/10dd73bb-3b33-4aa2-b1fa-9e6fbf725087)
      ![image](https://github.com/luismeramosr/app-sveltekit-code-challenge/assets/41213455/ec14563e-0476-48b9-beeb-1ecb87e27f0e)
      
**Completar tu solución**

**Subir tu solución**
      ![image](https://github.com/luismeramosr/app-sveltekit-code-challenge/assets/41213455/d1e48509-208e-43d8-bddc-849c51e722c0)
      ![image](https://github.com/luismeramosr/app-sveltekit-code-challenge/assets/41213455/2fa8427b-62ec-43b9-8470-eb5fdae5173d)
      ![image](https://github.com/luismeramosr/app-sveltekit-code-challenge/assets/41213455/101f40d0-b450-4a8e-8289-c6d1f59d1e90)
      ![image](https://github.com/luismeramosr/app-sveltekit-code-challenge/assets/41213455/2aa984a4-a9bd-4d75-bc26-1b556ba14766)
      ![image](https://github.com/luismeramosr/app-sveltekit-code-challenge/assets/41213455/f7309059-be21-4ef6-b7cf-3f767cf9eb92)



