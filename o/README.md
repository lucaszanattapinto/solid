# Open/Closed Principle

> Modules should be open for extension, but closed for modification

> If you can conform to this principle, then when you add a new feature to an application, you should be able to do that by writing new code and not changing any old code.

O sintoma mais evidente para esse problema é o encadeamento muito grande de `ifs` e `elifs`

```python
def validate(country_code):
    # ...
    # fields validations
    # ...

	if country_code == 'BR':
        # validate supplier for br
    else:
        # validate supplier for cl
```

O exemplo ilustra uma função de validação que se comporta de maneira diferente de acordo com o país. Nesse caso, o que acontece se o sistema suportar mais um país, por exemplo, Colombia? Temos que adicionar um `elif`, ou se a validação corresponder à de algum país, adicionar um `or` em um dos `ifs`? :poop:

```python
class ISupplierValidator(ABC):
    error_message = 'Supplier does not exist'

    @abstractmethod
    def validate(self) -> bool:
        raise NotImplementedError


class SupplierValidatorByTax(ISupplierValidator):
    def validate(self):
        # validate supplier by tax identification


class SupplierValidatorByName(ISupplierValidator):
    def validate(self):
        # validate supplier by name

def get_supplier_validator(self, country_code) -> ISupplierValidator:
    if country_code == 'BR':
        return SupplierValidatorByTax()
    elif country_code == 'CL':
        return SupplierValidatorByName()

def validate(country_code):
    # ...
    # fields validations
    # ...

    validator = get_supplier_validator(country_code)
    validator.validate()
```

Dessa forma, a função `validate` está fechada para modificação, mas aberta para extensão.  
PS.: O `ISupplierValidator` é opcional, pois como se trata de python, o polimorfismo pode ser realizado através do `duck typing`
