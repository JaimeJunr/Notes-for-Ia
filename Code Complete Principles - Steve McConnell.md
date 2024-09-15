# Code Complete Principles - Steve McConnell

## Overview
*Code Complete* é um guia abrangente para o desenvolvimento de software, enfatizando a criação de código de alta qualidade através de boas práticas de construção, design e manutenção. A obra oferece estratégias detalhadas sobre como escrever software limpo, eficiente e sustentável. Abaixo estão os principais conceitos e práticas descritos no livro.

---

## 1. **Importance of Software Construction**
   - A fase de construção é onde a maior parte do tempo de um projeto de software é gasta.
   - Escrever código bem estruturado, eficiente e fácil de manter reduz significativamente o custo do ciclo de vida de um software.
   - Atenção às boas práticas de programação minimiza o retrabalho e acelera a entrega de software de qualidade.

---

## 2. **Design Before Coding**
   - Um bom design define a estrutura do código, prevendo problemas antes que eles surjam.
   - Use diagramas de classes, fluxogramas e pseudocódigo para visualizar a solução antes de codificar.
   - Divida problemas grandes em partes menores e mais gerenciáveis, favorecendo a modularidade.

---

## 3. **Good Variable Naming**
   - Escolha nomes de variáveis que transmitam significado e contexto.
   - Nomes curtos são aceitáveis em escopos limitados, mas devem ser evitados em grandes blocos de código.
   - Utilize convenções consistentes para tipos de dados e estruturas.
   - Exemplo:
     ```python
     # Bad
     x = calculate(10, 20)
     
     # Good
     totalRevenue = calculateRevenue(weeklySales, taxRate)
     ```

---

## 4. **Writing High-Quality Routines**
   - Funções e métodos devem ser coesos e realizar uma tarefa bem definida.
   - Assegure que o número de parâmetros seja mínimo, idealmente entre zero e três.
   - Routines should have strong cohesion and loose coupling—each routine should focus on a single task.
   - Example:
     ```python
     # Bad
     def processOrder(order, user, db, emailService):
         # Does too many things: validation, database, email logic.
     
     # Good
     def validateOrder(order): ...
     def saveOrderToDB(order, db): ...
     def sendOrderEmail(order, emailService): ...
     ```

---

## 5. **Structured Programming**
   - Utilize controles de fluxo como `if`, `while`, `for`, e evite o uso de `goto`.
   - Funções bem estruturadas facilitam a leitura e compreensão.
   - Evite múltiplos níveis de aninhamento, simplifique fluxos de decisão.
   - Exemplo:
     ```python
     # Bad
     if user.isLoggedIn():
         if user.isVerified():
             if not user.isBanned():
                 # Execute logic
     
     # Good
     if not (user.isLoggedIn() and user.isVerified() and not user.isBanned()):
         return
     # Execute logic
     ```

---

## 6. **Minimizing Complexity**
   - Reduza a complexidade ciclomatica mantendo funções e módulos simples.
   - Limite o número de condições e loops dentro de uma única função.
   - Simplifique e divida tarefas complexas em componentes menores.
   - Exemplo:
     ```python
     # Bad
     def calculate(order, discount, tax, delivery, membership):
         # Lots of conditional logic
     
     # Good
     def applyDiscount(order): ...
     def calculateTax(order): ...
     def processMembership(order): ...
     ```

---

## 7. **Defensive Programming**
   - Antecipe erros e garanta que o sistema seja resiliente a falhas inesperadas.
   - Valide entradas em todos os níveis do sistema.
   - Lide com exceções de maneira clara e apropriada, evitando que o sistema quebre.
   - Exemplo:
     ```python
     # Bad
     def readFile(filePath):
         file = open(filePath, 'r')
     
     # Good
     def readFile(filePath):
         try:
             file = open(filePath, 'r')
         except IOError as e:
             log_error(e)
             raise
     ```

---

## 8. **Code Simplicity**
   - Escreva código que seja fácil de entender e de modificar por outros desenvolvedores.
   - Evite "clever code" que pode ser eficiente, mas difícil de manter.
   - Priorize a legibilidade em vez de otimizações prematuras.
   - Exemplo:
     ```python
     # Bad
     if x > 5 and x < 10: return True else: return False
     
     # Good
     return 5 < x < 10
     ```

---

## 9. **Refactoring**
   - Refatorar é melhorar a estrutura interna do código sem alterar seu comportamento externo.
   - Refatore regularmente para reduzir a dívida técnica e manter o código limpo.
   - Divida grandes funções em funções menores e mais simples.
   - Exemplo:
     ```python
     # Before Refactor
     def processOrder(order):
         # Large function with many responsibilities
     
     # After Refactor
     def validateOrder(order): ...
     def calculateTotal(order): ...
     def processOrder(order):
         validateOrder(order)
         calculateTotal(order)
     ```

---

## 10. **Code Reviews and Pair Programming**
   - Realize revisões de código regulares para identificar problemas e oportunidades de melhoria.
   - O feedback externo melhora a qualidade e a consistência do código.
   - Práticas como pair programming podem aumentar a colaboração e a troca de conhecimento entre desenvolvedores.

---

## 11. **Testing**
   - Teste o código frequentemente e de forma abrangente, cobrindo casos normais, limites e erros.
   - Escreva testes unitários para validar o comportamento de funções e classes isoladamente.
   - O teste ajuda a garantir que o código continue funcionando corretamente após alterações.
   - Exemplo:
     ```python
     def testCalculateTax():
         assert calculateTax(100, 0.1) == 10
         assert calculateTax(200, 0.05) == 10
     ```

---

## 12. **Managing Complexity with Abstraction**
   - Utilize abstrações para ocultar detalhes de implementação complexos.
   - Defina interfaces claras para que diferentes partes do sistema possam interagir de forma coesa e sem dependências fortes.
   - Exemplo:
     ```python
     # Abstraction via Interface
     class Database:
         def connect(self): ...
         def query(self, queryString): ...

     class MySQLDatabase(Database):
         def connect(self): ...
         def query(self, queryString): ...
     ```

---

## 13. **Estimating and Planning**
   - Estime o tempo de desenvolvimento baseado em experiências anteriores e decomponha tarefas grandes em partes menores e gerenciáveis.
   - Crie cronogramas realistas e leve em consideração possíveis atrasos e imprevistos.
   - A estimativa precisa ajuda a evitar prazos irrealistas e crises de última hora.

---

## 14. **Optimizing Performance**
   - Faça otimizações de desempenho apenas quando necessário e com base em medições reais.
   - Evite otimizações prematuras que possam prejudicar a legibilidade e a manutenção.
   - Priorize a clareza do código, focando em otimizações somente após identificar gargalos de desempenho.

---

## 15. **Conclusion**
   *Code Complete* ensina a construção de software a partir de uma base sólida de princípios e práticas, promovendo código simples, legível, modular e fácil de manter. O livro incentiva a aplicação de padrões consistentes para reduzir a complexidade e melhorar a qualidade geral dos projetos de software.

---

## Additional Resources
- **Book**: "Code Complete: A Practical Handbook of Software Construction" by Steve McConnell
- **Website**: Steve McConnell's blog and resources on software engineering.
