
# MOCK

## Patch fungsi menggunakan decorators

### mock class

mock_1.py
```python
import random
import unittest
import mock

def random_choice(choices):
	return choices[-1]

class TestRandom(unittest.TestCase):
	@mock.patch('random.choice', side_effect=random_choice)
	def test_random_choice(self, random_choice_function):
		assert random.choice([1, 2, 3]) == 3

if __name__ == "__main__":
	unittest.main()
```

jalankan `python mock_1.py`

- `side_effect` digunakan untuk me-replace fungsi dengan fungsi baru
- decorator menambahkan argumen baru `random_choice_function` untuk method yang di patch
- patch diatas berlaku juga jika kita meng-import fungsi yang menggunakan `random.choice`


### mock method
menggunakan `__main__`

mock_1.py
```python
from random import choice
import unittest
import mock

def random_choice(choices):
	return choices[-1]

class TestRandom(unittest.TestCase):
	@mock.patch('__main__.choice', side_effect=random_choice)
	def test_random_choice(self, random_choice_function):
		assert choice([1, 2, 3]) == 3

if __name__ == "__main__":
	unittest.main()
```

### mock method di modul lain

helper_1.py
```python
from random import choice

def get_random(choices):
	return choice(choices)
```

mock_1.py
```python
from helper_1 import get_random
import unittest
import mock

def random_choice(choices):
	return choices[-1]

class TestRandom(unittest.TestCase):
	@mock.patch('helper_1.choice', side_effect=random_choice)
	def test_random_choice(self, random_choice_function):
		assert get_random([1, 2, 3]) == 3

if __name__ == "__main__":
	unittest.main()
```

### return value
tidak menggunakan side_effect

```python
import random
import unittest
import mock

def random_choice(choices):
	return choices[-1]

class TestRandom(unittest.TestCase):
	@mock.patch('random.choice', return_value=5)
	def test_random_choice(self, random_choice_function):
		assert random.choice([1, 2, 3]) == 5

if __name__ == "__main__":
	unittest.main()
```

## Patch fungsi menggunakan context managers
