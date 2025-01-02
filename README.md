# Proyecto Django con DRF y DRF-Spectacular

Este proyecto utiliza Django, Django Rest Framework (DRF) y DRF-Spectacular para crear un CRUD completo con una documentación automatizada de la API. Contiene dos aplicaciones relacionadas mediante una clave foránea: `app1` (Autores) y `app2` (Libros).

## Requisitos

- Python 3.8 o superior
- Django 4.0 o superior
- Django Rest Framework
- DRF-Spectacular

## Instalación

1. **Clona el repositorio**:

   ```bash
   git clone <URL-del-repositorio>
   cd <nombre-del-directorio>
   ```

2. **Crea un entorno virtual**:

   ```bash
   python -m venv venv
   source venv/bin/activate  # En Windows: venv\Scripts\activate
   ```

3. **Instala las dependencias**:

   ```bash
   pip install -r requirements.txt
   ```

4. **Realiza las migraciones**:

   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

5. **Inicia el servidor**:

   ```bash
   python manage.py runserver
   ```

## Estructura del Proyecto

```
project/
├── app1/
│   ├── models.py       # Modelo Author
│   ├── serializers.py  # Serializador Author
│   ├── views.py        # Vista CRUD para Author
├── app2/
│   ├── models.py       # Modelo Book
│   ├── serializers.py  # Serializador Book
│   ├── views.py        # Vista CRUD para Book
├── docs/               # Configuración de DRF-Spectacular
├── project/
│   ├── settings.py     # Configuración principal
│   ├── urls.py         # Rutas principales
├── manage.py
```

## Endpoints

### CRUD de Autores

- **GET** `/rest/authors/` - Lista de autores
- **POST** `/rest/authors/` - Crear un nuevo autor
- **GET** `/rest/authors/{id}/` - Obtener un autor por ID
- **PUT** `/rest/authors/{id}/` - Actualizar un autor
- **DELETE** `/rest/authors/{id}/` - Eliminar un autor

### CRUD de Libros

- **GET** `/rest/books/` - Lista de libros
- **POST** `/rest/books/` - Crear un nuevo libro
- **GET** `/rest/books/{id}/` - Obtener un libro por ID
- **PUT** `/rest/books/{id}/` - Actualizar un libro
- **DELETE** `/rest/books/{id}/` - Eliminar un libro

### Documentación de la API

- **Esquema JSON**: `/api/schema/`
- **Swagger UI**: `/api/swagger-ui/`
- **Redoc**: `/api/redoc/`

## Configuración de DRF-Spectacular

En `settings.py`, asegúrate de incluir la configuración para `DEFAULT_SCHEMA_CLASS`:

```python
REST_FRAMEWORK = {
    'DEFAULT_SCHEMA_CLASS': 'drf_spectacular.openapi.AutoSchema',
}

INSTALLED_APPS = [
    ...,
    'rest_framework',
    'drf_spectacular',
    'app1',
    'app2',
    'docs',
]
```

### Rutas de Documentación

En `docs/urls.py`:

```python
from django.urls import path
from drf_spectacular.views import SpectacularAPIView, SpectacularSwaggerView, SpectacularRedocView

urlpatterns = [
    path('schema/', SpectacularAPIView.as_view(), name='schema'),
    path('swagger-ui/', SpectacularSwaggerView.as_view(url_name='schema'), name='swagger-ui'),
    path('redoc/', SpectacularRedocView.as_view(url_name='schema'), name='redoc'),
]
```

Inclúyelas en las rutas principales (`project/urls.py`):

```python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('rest/', include(router.urls)),
    path('api/', include('docs.urls')),
]
```

## Dependencias

Lista de paquetes utilizados:

```plaintext
Django
Django Rest Framework
drf-spectacular
```

## Notas

- Asegúrate de reiniciar el servidor después de realizar cambios en la configuración.
- Puedes extender la funcionalidad añadiendo más aplicaciones o relaciones según sea necesario.

¡Listo! Ahora tienes un proyecto funcional con un CRUD completo y documentación de API automatizada.
