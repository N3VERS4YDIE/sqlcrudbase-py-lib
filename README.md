# sqlcrudbase (Python Library)

A lightweight, flexible, and reusable Python library designed to simplify the creation of CRUD (Create, Read, Update, Delete) operations in FastAPI applications. It leverages **Pydantic** for request and response validation and **Peewee** as the ORM for managing database interactions.

## Features

- **Pre-built CRUD Operations**: Simplifies the process of setting up standard CRUD routes.
- **FastAPI Integration**: Easily create FastAPI routes with minimal code.
- **Pydantic & Peewee**: Handles data validation with Pydantic and works with Peewee for database operations.
- **Modular Structure**: Decouples controller, service, and repository layers for better maintainability.

## Installation

Install the package directly from PyPI using pip:

```bash
pip install sqlcrudbase
```

## Usage

### Setting up a Controller

The `BaseController` provides a set of standard CRUD operations for your FastAPI application. Here’s how you can use it:

```python
from my_models import MyPydanticModel, MyPeeweeModel
from sqlcrudbase import BaseController, BaseService

# Create a service
service = BaseService(MyPeeweeModel)

# Create a controller
controller = BaseController(MyPydanticModel, MyPeeweeModel, service)

# Add routes to your FastAPI app
app = FastAPI()
app.include_router(controller.get_router(), prefix="/items")
```

### Defining the Models

You need to define your **Pydantic** model (for validation) and your **Peewee** model (for database interactions). For example:

```python
from peewee import Model, CharField, IntegerField
from pydantic import BaseModel

class MyPeeweeModel(Model):
    name = CharField()
    quantity = IntegerField()

class MyPydanticModel(BaseModel):
    name: str
    quantity: int
```

### Example Routes

- **Create an Item**: `POST /items`
- **Get All Items**: `GET /items`
- **Get Item by ID**: `GET /items/{id}`
- **Update Item by ID**: `PUT /items/{id}`
- **Delete Item by ID**: `DELETE /items/{id}`

## How it Works

### BaseController

The `BaseController` class defines the FastAPI routes and links them to the appropriate service methods:

- `POST /`: Create a new item.
- `GET /`: Retrieve all items.
- `GET /{id}`: Retrieve an item by its ID.
- `PUT /{id}`: Update an existing item by its ID.
- `DELETE /{id}`: Delete an item by its ID.

### BaseService

The `BaseService` contains the business logic and interacts with the repository for database operations. It includes methods for:

- Retrieving all records.
- Retrieving a record by ID.
- Creating a new record.
- Updating an existing record.
- Deleting a record by ID.

### BaseRepository

The `BaseRepository` interacts directly with the database using Peewee. It provides methods for:

- Retrieving all records.
- Retrieving a record by ID.
- Creating a new record.
- Deleting a record by ID.

## Extending the Library

You can easily extend this library by adding more specific logic to the service or overriding any of the CRUD methods.

For example, to add custom validation or processing logic before creating a model:

```python
class CustomService(BaseService):
    def create(self, model: dict):
        # Custom validation logic here
        return super().create(model)
```

## Contributing

Contributions are welcome! Feel free to open issues or submit pull requests to improve this library.

### References

- **Peewee (ORM for Python)**  
  GitHub: [https://github.com/coleifer/peewee](https://github.com/coleifer/peewee)  
  Documentation: [http://docs.peewee-orm.com/](http://docs.peewee-orm.com/)

- **Pydantic (Data validation and settings management)**  
  GitHub: [https://github.com/pydantic/pydantic](https://github.com/pydantic/pydantic)  
  Documentation: [https://docs.pydantic.dev/](https://docs.pydantic.dev/)

## License

This project is licensed under the [MIT LICENSE](https://github.com/N3VERS4YDIE/sqlcrudbase-py-lib/blob/main/LICENSE).
