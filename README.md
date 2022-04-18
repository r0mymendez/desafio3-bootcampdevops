# Desafio Devops

El proyecto contiene una aplicación básica con Node, Ngnix y MySQL.

Con cada actualización de la página, se registrará un nuevo registro en la base de datos y se mostrará en la lista, en la misma página.

El proyecto contiene algunas falencias y errores, analizar e implementar las correcciones correspondientes.

Si no entiendes algún concepto o parte del problema, ¡no hay de qué preocuparse! Queremos que aceptes el desafío hasta donde sepas.

### ¿Lo que debe hacerse? ### 

 - ajustes que hacen que todas las aplicaciones se levanten y se comuniquen
 - un README que contiene información sobre el problema a lo largo del proyecto para identificar y corregir errores

Comprométase en el camino para que podamos entender su forma de pensar!! :)
 
---

### 📝 Solución: 🙋🏻‍♀️ Romina Mendez (r0mymendez)

1. **docker-compose:** Agregar networks: **Docker Engine** tiene un conjunto de driver que permiten crear configuraciones de redes y una de ella es **bridge** que es la que permite comunicar a los contenedores entre si.

   ```Dockerfile
   networks: 
        node-network:
            driver: bridge
   ```
2. **docker-compose:** Agregar el port al contenedor de MYSQL
   ```Dockerfile
    ports:
        - "3306:3306"
    ```

3. **DockerFile**: Se agrega la siguiente sintaxis que es el que va a instalar todos los paquetes que estan definidos en el archivo **package.json**
 ```Dockerfile
    RUN npm install

 ```

4. **DockerFile**: Modificar el entrypoint que es el que especifica que ejecutable va utilizar el contendor.

   ```Dockerfile
    ENTRYPOINT ./docker-entrypoint.sh
   ```

5.  **connectionDb.js**: Se modifica la base de datos, que se puede validar desde el archivo `/mysql/init.sql` y la denominación del esquema de la base de datos es `node_db`

    ```js
    database: process.env.DATABASE || 'node_db'
    ```

6. Ejecutar `docker-compose up --build` para construir las imagenes e iniciar los contenedores.
7. Ingresar a `http://localhost:3000/`

<img width="1433" alt="image" src="https://user-images.githubusercontent.com/39013829/163893173-b085bf30-ac2b-431c-bfb5-26af7ab6dec7.png">
