# Adapter Method

A adapter method is used to create a bridge between two incompatible interfaces.

### Terminology:
1. **Adaptee**: The class that needs to be made compatible with the client interface
2. **Client Interface**: Interface with methods to be implemented by the client
3. **Client**: Class that implements the methods
4. **Adapter**: The classs that makes it possible for the Client and Adaptee to collaborate

### Example:
```python
class ShoppingCart:
	def get_total_price(self, price: int) -> int:
		return price * 10
		
class UserCart:
	def get_full_price(self, price: int) -> int:
		return price * 10
```

```python
class ShoppingCartAdapter:
	def __init__(self, user_cart: UserCart):
		self.cart = user_cart
	def get_total_price(self, price: int) -> int:
		return self.cart.get_full_price(price=price)
```

Now we can invoke `get_total_price` on a `UserCart` by passing an instance of it to a `ShoppingCartAdapter`

```python
cart = UserCart()
user_cart = ShoppingCartAdapter(cart)

user_cart.get_total_price(price=100)
```

```d
>> 100
```
