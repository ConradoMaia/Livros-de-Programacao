# Padrões de Projetos (Design Patterns) - Erich Gamma et al.

## Anotações (rascunho)

- Livro clássico GoF (Gang of Four).
- Divisão em **3 categorias principais**:
  - **Criação**: lidar com instanciamento de objetos.
  - **Estruturais**: composição de classes e objetos.
  - **Comportamentais**: interação e responsabilidade entre objetos.

---

## Padrões de Criação
- **Factory Method** → cria objetos sem expor lógica de criação.
- **Abstract Factory** → cria famílias de objetos relacionados.
- **Builder** → separa construção de um objeto complexo de sua representação.
- **Prototype** → cria novos objetos a partir de um protótipo.
- **Singleton** → garante única instância global.

## Padrões Estruturais
- **Adapter** → converte interface de uma classe para outra esperada.
- **Composite** → objetos em estrutura de árvore.
- **Decorator** → adicionar responsabilidades dinamicamente.
- **Proxy** → objeto substituto para controlar acesso.
- **Bridge** → separa abstração da implementação.
- **Facade** → interface simples para subsistemas complexos.
- **Flyweight** → otimiza uso de muitos objetos pequenos.

## Padrões Comportamentais
- **Observer** → dependência 1:N entre objetos.
- **Strategy** → encapsula algoritmos intercambiáveis.
- **Command** → encapsula requisições como objetos.
- **Template Method** → define esqueleto de algoritmo, subclasses preenchem detalhes.
- **State** → altera comportamento baseado em estado interno.
- **Iterator** → percorre coleções sem expor detalhes.
- **Chain of Responsibility** → passa requisições em cadeia até alguém tratar.
- **Mediator** → centraliza a comunicação entre objetos.
- **Memento** → captura/restaura estado interno.
- **Visitor** → adiciona operações sem modificar classes existentes.
- **Interpreter** → define gramática e interpretador.

---

## Observações gerais
- “Programe para interfaces, não para implementações”.
- “Prefira composição ao invés de herança”.
- MVC é exemplo prático que usa Strategy, Observer e Composite.
- Muito usado em entrevistas e arquitetura de sistemas.

---

## Exemplos de Código (em Python)

### Singleton
```python
class Singleton:
    _instance = None
    def __new__(cls, *args, **kwargs):
        if not cls._instance:
            cls._instance = super().__new__(cls)
        return cls._instance

obj1 = Singleton()
obj2 = Singleton()
print(obj1 is obj2)  # True
```

### Observer
```python
class Observer:
    def update(self, message):
        print(f"Notificado: {message}")

class Subject:
    def __init__(self):
        self._observers = []
    def add_observer(self, obs):
        self._observers.append(obs)
    def notify(self, msg):
        for obs in self._observers:
            obs.update(msg)

subj = Subject()
obs1, obs2 = Observer(), Observer()
subj.add_observer(obs1)
subj.add_observer(obs2)
subj.notify("Novo evento!")
```

### Strategy
```python
class Strategy:
    def execute(self, a, b): pass

class Soma(Strategy):
    def execute(self, a, b): return a + b

class Multiplica(Strategy):
    def execute(self, a, b): return a * b

class Contexto:
    def __init__(self, strategy):
        self.strategy = strategy
    def calcular(self, a, b):
        return self.strategy.execute(a, b)

c1 = Contexto(Soma())
print(c1.calcular(2, 3))  # 5
c2 = Contexto(Multiplica())
print(c2.calcular(2, 3))  # 6
```

