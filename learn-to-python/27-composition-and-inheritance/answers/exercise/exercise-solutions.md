# Exercise Solutions: Composition and Inheritance

```python
from abc import ABC, abstractmethod
from math import pi
from typing import Protocol

class Writer(Protocol):
    def write(self, text: str) -> None:
        pass

class MemoryWriter:
    def __init__(self) -> None:
        self.messages: list[str] = []

    def write(self, text: str) -> None:
        self.messages.append(text)

class ReportService:
    def __init__(self, writer: Writer) -> None:
        self._writer = writer

    def create(self, title: str) -> None:
        self._writer.write(f"Report: {title}")

class Named:
    def __init__(self, name: str) -> None:
        self.name = name

class Shape(Named, ABC):
    @abstractmethod
    def area(self) -> float:
        pass

class Rectangle(Shape):
    def __init__(self, width: float, height: float) -> None:
        super().__init__("rectangle")
        self.width = width
        self.height = height

    def area(self) -> float:
        return self.width * self.height

class Circle(Shape):
    def __init__(self, radius: float) -> None:
        super().__init__("circle")
        self.radius = radius

    def area(self) -> float:
        return pi * self.radius ** 2

def print_area(shape: Shape) -> None:
    print(shape.name, shape.area())

writer = MemoryWriter()
service = ReportService(writer)
service.create("Weekly status")
print(writer.messages)
print_area(Rectangle(3, 4))
print_area(Circle(2))
```

Both concrete shapes can replace `Shape` because each supplies the promised `area` behavior. Their constructors use `super` to share valid name initialization.

ReportService composes a writer because it uses a separate capability rather than becoming a writer. Making ReportService inherit MemoryWriter would incorrectly claim that every report service is itself a writer. Composition keeps report creation and message storage as separate responsibilities and makes the in-memory test direct.
