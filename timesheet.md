Я сделал вспомогательный класс Record, чтобы код чуть проще читался, но можно было обойтись и без него, чуток усложнив саму структуру хранения обработанных данных

```python
from collections import defaultdict


class Record:

    def __init__(self):
        self.history: list[int] = []
    
    def add(self, hours: int):
        self.history.append(hours)

    @property
    def sum(self):
        return sum(self.history)

    @property
    def history_verbose(self) -> str:
        return ', '.join(str(i) for i in self.history)


def parse_input(data: str) -> defaultdict:
    # Разбиваем на строки
    # strip нужен, чтобы убрать \n по краям
    rows = data.strip().split('\n')

    result = defaultdict(Record)
    for row in rows:
        name, hours = row.rsplit(' ', 1)
        result[name].add(int(hours))

    return result


def make_output(data: dict[str, Record]):
    for name, record in data.items():
        print(f'{name}: {record.history_verbose}; sum: {record.sum}')


if __name__ == '__main__':
    # Прибиваем к левому краю, чтобы не было лишних пробелов))
    input_data = """
Андрей 9
Василий 11
Василий 29
Роман 7
X Æ A-12 45
Иван Петров 3
Андрей 6
Роман 11
    """
    prepared_data = parse_input(input_data)
    make_output(prepared_data)

```

Тут ещё многое может зависеть от формата входных данных и от самого источника (файл, stdin), но я сделал самый простой вариант.
