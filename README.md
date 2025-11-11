# POOJavaDio

# Sistema de Bootcamp - Desafio POO em Java

<div align="center">

![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![POO](https://img.shields.io/badge/POO-4%20Pilares-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge)

**Desmistificando a Programação Orientada a Objetos com Java**

[Sobre](#-sobre) • [Pilares da POO](#-pilares-da-poo) • [Estrutura](#-estrutura-do-projeto) • [Como Usar](#-como-usar) • [Exemplos](#-exemplos-de-uso) • [Evoluções](#-possíveis-evoluções)

</div>

---

## 📖 Sobre

Este projeto é uma implementação prática dos **4 pilares da Programação Orientada a Objetos (POO)** através de um sistema de gerenciamento de Bootcamps. O sistema permite criar cursos, mentorias, inscrever desenvolvedores e acompanhar seu progresso através de um sistema de XP.

### 🎯 Objetivo

Demonstrar na prática os conceitos fundamentais da POO:
- ✅ **Abstração**
- ✅ **Encapsulamento**
- ✅ **Herança**
- ✅ **Polimorfismo**

---

## 🏛️ Pilares da POO

### Abstração

```java
abstract class Conteudo {
    protected static final double XP_PADRAO = 10d;
    private String titulo;
    private String descricao;
    
    public abstract double calcularXp();
}
```

**O que é?** Processo de identificar características essenciais de um objeto, ignorando detalhes irrelevantes.

**No projeto:** A classe `Conteudo` abstrai o conceito genérico de conteúdo educacional, definindo apenas o que é comum entre Cursos e Mentorias.

---

### Encapsulamento

```java
class Dev {
    private String nome; // Atributo privado
    private Set<Conteudo> conteudosInscritos = new LinkedHashSet<>();
    
    public String getNome() { // Acesso controlado
        return nome;
    }
}
```

**O que é?** Ocultar os detalhes internos de implementação e expor apenas o necessário.

**No projeto:** Todos os atributos são privados e acessados através de getters/setters, protegendo a integridade dos dados.

---

### Herança

```java
class Curso extends Conteudo {
    private int cargaHoraria;
    // Herda titulo, descricao e XP_PADRAO
}

class Mentoria extends Conteudo {
    private LocalDate data;
    // Herda titulo, descricao e XP_PADRAO
}
```

**O que é?** Mecanismo que permite criar novas classes baseadas em classes existentes.

**No projeto:** `Curso` e `Mentoria` herdam comportamentos comuns de `Conteudo`, evitando duplicação de código.

---

### Polimorfismo

```java
// Curso
@Override
public double calcularXp() {
    return XP_PADRAO * cargaHoraria; // XP baseado em horas
}

// Mentoria
@Override
public double calcularXp() {
    return XP_PADRAO + 20d; // XP fixo com bônus
}
```

**O que é?** Capacidade de objetos de classes diferentes responderem de forma única ao mesmo método.

**No projeto:** Cada tipo de conteúdo calcula XP de forma diferente, mas usa a mesma interface.

---

## 📁 Estrutura do Projeto

```
bootcamp-poo/
│
├── Conteudo.java          (Classe Abstrata)
│   ├── Curso.java         (Herança)
│   └── Mentoria.java      (Herança)
│
├── Dev.java               (Classe Concreta)
├── Bootcamp.java          (Classe Concreta)
└── Main.java              (Programa Principal)
```

### Descrição das Classes

| Classe | Tipo | Responsabilidade |
|--------|------|------------------|
| `Conteudo` | Abstrata | Define estrutura base para conteúdos educacionais |
| `Curso` | Concreta | Representa cursos com carga horária |
| `Mentoria` | Concreta | Representa mentorias com data específica |
| `Dev` | Concreta | Gerencia desenvolvedores e seu progresso |
| `Bootcamp` | Concreta | Organiza conteúdos e gerencia inscrições |

---

## Como Usar

### Pré-requisitos

- Java JDK 8 ou superior
- IDE (IntelliJ IDEA, Eclipse, VS Code) ou terminal

### Executando o Projeto

1. **Clone ou baixe o arquivo Main.java**

2. **Compile o código:**
```bash
javac Main.java
```

3. **Execute:**
```bash
java Main
```

---

## Exemplos de Uso

### Criando um Curso

```java
Curso cursoJava = new Curso();
cursoJava.setTitulo("Curso Java Avançado");
cursoJava.setDescricao("Aprenda Java do zero ao avançado");
cursoJava.setCargaHoraria(40);

// XP do curso: 10 * 40 = 400 XP
```

### Criando uma Mentoria

```java
Mentoria mentoria = new Mentoria();
mentoria.setTitulo("Mentoria de Carreira");
mentoria.setDescricao("Como se destacar no mercado");
mentoria.setData(LocalDate.now());

// XP da mentoria: 10 + 20 = 30 XP
```

### Criando um Bootcamp

```java
Bootcamp bootcamp = new Bootcamp();
bootcamp.setNome("Bootcamp Java Developer");
bootcamp.setDescricao("Formação completa em Java");
bootcamp.getConteudos().add(cursoJava);
bootcamp.getConteudos().add(mentoria);
```

### Inscrevendo um Dev

```java
Dev dev = new Dev();
dev.setNome("Maria");
dev.inscreverBootcamp(bootcamp);

// Progredindo nos conteúdos
dev.progredir(); // Completa primeiro conteúdo
dev.progredir(); // Completa segundo conteúdo

// Calculando XP total
double xpTotal = dev.calcularTotalXp();
System.out.println("XP Total: " + xpTotal);
```

---

## Diagrama de Classes (Conceitual)

```
                    ┌─────────────┐
                    │  Conteudo   │ (Abstrata)
                    ├─────────────┤
                    │ - titulo    │
                    │ - descricao │
                    ├─────────────┤
                    │ + calcularXp() │ (Abstrato)
                    └──────┬──────┘
                           │
              ┌────────────┴────────────┐
              │                         │
      ┌───────▼───────┐         ┌──────▼──────┐
      │     Curso     │         │   Mentoria  │
      ├───────────────┤         ├─────────────┤
      │- cargaHoraria │         │ - data      │
      ├───────────────┤         ├─────────────┤
      │+ calcularXp() │         │+ calcularXp()│
      └───────────────┘         └─────────────┘

┌──────────────┐                    ┌─────────────┐
│     Dev      │◄───inscrito────────┤  Bootcamp   │
├──────────────┤                    ├─────────────┤
│ - nome       │                    │ - nome      │
│ - conteudos  │                    │ - descricao │
├──────────────┤                    │ - conteudos │
│ + progredir()│                    │ - devs      │
│ + calcularXp()│                   └─────────────┘
└──────────────┘
```

---

##  Funcionalidades

- [x] Criar cursos com carga horária personalizada
- [x] Criar mentorias com datas específicas
- [x] Organizar bootcamps com múltiplos conteúdos
- [x] Inscrever desenvolvedores em bootcamps
- [x] Sistema de progressão de conteúdos
- [x] Cálculo automático de XP
- [x] Validação de progressão (não permite progredir sem inscrição)

---

##  Possíveis Evoluções

### Nível Básico
- [ ] Adicionar campo de categoria aos conteúdos
- [ ] Implementar método para listar todos os devs de um bootcamp
- [ ] Adicionar status ao bootcamp (aberto/fechado)

### Nível Intermediário
- [ ] Sistema de certificados ao concluir bootcamp
- [ ] Níveis de dificuldade (Iniciante, Intermediário, Avançado)
- [ ] Pré-requisitos entre cursos
- [ ] Sistema de avaliações (notas de 0-10)

### Nível Avançado
- [ ] Ranking de desenvolvedores por XP
- [ ] Sistema de badges e conquistas
- [ ] Integração com banco de dados
- [ ] API REST para gerenciamento
- [ ] Interface gráfica (JavaFX ou Swing)
- [ ] Sistema de notificações
- [ ] Relatórios de progresso em PDF

---

##  Tecnologias Utilizadas

- **Linguagem:** Java
- **Paradigma:** Programação Orientada a Objetos
- **Collections:** Set, LinkedHashSet, HashSet
- **API de Data:** LocalDate (Java 8+)
- **Streams:** Para cálculos funcionais

---

##  Conceitos Aplicados

### Design Patterns
- **Template Method:** Classe abstrata define estrutura, subclasses implementam detalhes

### Boas Práticas
- ✅ Nomes descritivos de classes e métodos
- ✅ Separação de responsabilidades
- ✅ Encapsulamento adequado
- ✅ Uso de Collections apropriadas
- ✅ Sobrescrita de `equals()` e `hashCode()`
- ✅ Uso de Optional para evitar NullPointerException

---

## Licença

Este projeto foi desenvolvido para fins educacionais e está livre para uso e modificação.

---

## Autor

Desenvolvido como parte do desafio de **Programação Orientada a Objetos em Java**. Por Larissa Campos Cardoso

---

<div align="center">

**Feito com ☕ e Java**

</div>
