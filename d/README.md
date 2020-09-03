# Dependency Inversion Principle

> High-level modules should not depend on low-level modules. Both should depend on abstractions (e.g. interfaces).
Abstractions should not depend on details. Details (concrete implementations) should depend on abstractions.

```python
class CSVInput:
    def format_payload(self):
        # formats csv payload


class OrderProcessor:
    def create_order(self, payload):
        formatted_payload = CSVInput().format_payload(payload)

```

Percebe-se que `create_order` depende de um tipo de payload específico. Se por ventura o tipo de payload mudar, `OrderProcessor` teria de ser refatorado.

```python
class Input(ABC):
    def format_payload():
        raise NotImplementedError()

class CSVInput(Input):
    def format_payload():
        # formats csv payload

class FormInput(Input):
    def format_payload():
        # formats form payload

class OrderProcessor:
    def __init__(payload_type: Input):
        self.payload_type = payload_type()

    def create_order(self, payload):
        formatted_payload = self.payload_type.format_payload(payload)
```

Criando uma abstração para o tipo de payload, a classe se torna flexível a ponto de aceitar qualquer tipo de payload, desde que ele siga a assinatura de `Input`.