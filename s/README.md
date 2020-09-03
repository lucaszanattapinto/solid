# Single Responsibility Principle

> A class should only have one reason to change

```python
class OrderFlowSerializer(serializers.ModelSerializer):
    # ...
    # serialize/deserialize methods
    # ...
    def create(self, validated_data):	
        OrderFlowHistoryStatus.objects.create(**validated_data)	
        return OrderFlowCurrentStatus.objects.create(**validated_data)	

    def update(self, instance, validated_data):	
        OrderFlowHistoryStatus.objects.create(**instance)	
        return super().update(validated_data, instance)
```

O exemplo acima representa uma classe que além de ter a responsabilidade de serialização, também é responsável por salvar o dado no banco. Nota-se que existe uma lógica amarrada à persistência do model. Isso implica que a via oficial de persistência do mesmo é um serializer (?).  
"Cada macaco no seu galho", como diria Gilberto Gil.  
Para corrigir o problema:

```python
class OrderFlowSerializer(serializers.ModelSerializer):
    # ...
    # serialize/deserialize methods
    # ...
```

```python
class OrderFlowCurrentStatus(models.Model):
    # ...
    # model attributes
    # ...

    def save(
        self,
        force_insert=False,
        force_update=False,
        using=None,
        update_fields=None,
    ):
        OrderFlowHistoryStatus.objects.create(
            order_id=self.order_id, status=self.status, user=self.user
        )
        return super().save(
            force_insert=force_insert,
            force_update=force_update,
            using=using,
            update_fields=update_fields,
        )
```