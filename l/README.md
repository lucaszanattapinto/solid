# Liskov Substitution Principle

> Se q(x) é uma propriedade demonstrável dos objetos x de tipo T. Então q(y) deve ser verdadeiro para objetos y de tipo S onde S é um subtipo de T.

![Mother of God](https://i.kym-cdn.com/entries/icons/facebook/000/004/029/motherofgod.jpg)

Traduzindo para o pt-br: classes derivadas devem ser substituíveis por suas classes bases sem nenhum colateral.  

Basicamente, esse princípio serve para nos alertar quanto a criação de abstrações problemáticas.

A forma mais simples de explicar esse princípio é com o exemplo do quadrado x retângulo

```python
class Rectangle:
    def set_height(self, value):
        self.height = value

    def set_width(self, value):
        self.width = value

class Square(Rectangle):
    def set_height(self, value):
        self.height = value
        self.width = value

    def set_width(self, value):
        self.height = value
        self.width = value

@pytest.mark.parametrize(
    'shape', [(Rectangle),(Square)]
)
def test_calculate_area(shape_type):
    shape = shape_type()
    shape.set_height(4)
    shape.set_width(5)
    assert shape.heigth * shape.width == 20
```

Esse teste vai falhar quando `shape_type` for `Square`, ou seja, de acordo com essa abstração, `Rectangle` não pode ser substituido por `Square`, o que viola o princípio em questão.  

