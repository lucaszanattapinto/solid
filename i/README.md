# Interface Segregation Principle

Esse princípio basicamente dita que o usuário de uma determinada classe não deve ser obrigado a implementar um método que não usa.

```python
class Beer(ABC):
    @abstractmethod
    def get_corn_amount(self):
        raise NotImplementedError

    @abstractmethod
    def get_hop_amount(self):
        raise NotImplementedError

    @abstractmethod
    def get_malt_amount(self):
        raise NotImplementedError

class NotSoGood(Beer):
    def get_corn_amount(self):
        return 'alot!'
    
    def get_hop_amount(self):
        return 'not sure if any'

    def get_malt_amount(self):
        return 'a little!'

class Niceru(Beer):
    def get_corn_amount(self):
        raise Exception('Niceru does not have corn in its formula')

    def get_hop_amount(self):
        return 'considerable amount'

    def get_malt_amount(self):
        return '100%'
```

Pelo exemplo acima, percebemos que a escolha dos métodos para `Beer` não é a melhor, pois nem todas as cervejas possuem milho em sua composição.  
Uma abordagem melhor talvez seria mais ou menos assim:

```python
class Beer(ABC):
    @abstractmethod
    def get_malt_amount(self):
        raise NotImplementedError

class Hop(ABC):
    @abstractmethod
    def get_hop_amount(self):
        raise NotImplementedError

class Corn(ABC):
    @abstractmethod
    def get_corn_amount(self):
        raise NotImplementedError

class NotSoGood(Beer, Hop, Corn):
    def get_corn_amount(self):
        return 'alot!'
    
    def get_hop_amount(self):
        return 'not sure if any'

    def get_malt_amount(self):
        return 'a little!'

class Niceru(Beer, Hop):
    def get_hop_amount(self):
        return 'considerable amount'

    def get_malt_amount(self):
        return '100%'
```