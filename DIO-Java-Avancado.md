# Java Avançado

## Paradigma Funcional no Java

*Requisitos básicos:*

- Conceitos básicos de java
- Orientação a objeto
- Java Generics
- Collections: List e Set

O paradigma funcional é processo de construir software através de composição de funções puras, evitando compartilhamento de estados, dados mutáveis e efeitos colaterais. É declarativa ao invés de imperativa, essa é a definição de Eric Elliot.

**Paradigma Imperativo:** E aquele que expressa o código através de comandos ao computador, nele é possível ter controle de estado dos objetos.

```java
class Imperativo{
    public static void main(String[] args){
        int valor = 10; //Instrução
        int resultado = valor * 3; //Instrução
        System.out.println("O resultado é: " + resultado);
    }
}
```

**Paradigma funcional:** Damos uma regra, uma declaração de como queremos que o programa se comporte.

```java
class Funcional{
    public static void main(String[] args){
        UnaryOperator<Integer> calculaValorVezes3 = valor -> valor * 3; //Conceito Paradigma Funcional
        int valor = 10;
        System.out.println("O resultado é: " + calculaValorVezes3.apply(10));
    }
}
```

### Conceitos Fundamentais da Programação Funcional

Composição de funções: 
