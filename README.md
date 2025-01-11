![Diagrama do Banco Digital - 3Core drawio](https://github.com/user-attachments/assets/fa3612c7-dcec-48c3-8142-f9c4db497cb3)


# Sistema de Gestão de Vendas: CRUD Completo com JPA, Hibernate, PostgreSQL e Testes Avançados


# CRUD Cliente, Produto e Vendas

Este projeto implementa um sistema CRUD completo para **Clientes**, **Produtos** e **Vendas**, utilizando tecnologias como **JPA**, **PostgreSQL**, **Docker**, **Hibernate**, com testes unitários e de integração, mocks, e Javadocs detalhados. O projeto segue boas práticas de arquitetura, como o uso de classes abstratas, DAOs, Services, e interfaces.

## Tecnologias Utilizadas

- **Java 21**
- **Spring Data**
- **JPA (Hibernate)**
- **PostgreSQL**
- **Docker**
- **JUnit 4 (Testes)**
- **Mockito (Mocks)**

## Estrutura do Projeto

O projeto está estruturado com as seguintes camadas e componentes:

- **Entidades**: Representação das tabelas no banco de dados (Cliente, Produto, Venda).
- **Interfaces**: Para garantir a implementação consistente das classes.
- **DAOs**: Responsáveis pela persistência e interação com o banco de dados via JPA.
- **Services**: Contêm a lógica de negócios, utilizando os DAOs para acessar os dados.
- **Testes**: Testes unitários e de integração para garantir o correto funcionamento do sistema.
- **Mocks**: Utilização de Mockito para simular dependências externas durante os testes.
- **Javadocs**: Documentação do código.

## Funcionalidades

- **CRUD para Cliente**: Cadastro, leitura, atualização e exclusão de clientes.
- **CRUD para Produto**: Cadastro, leitura, atualização e exclusão de produtos.
- **CRUD para Vendas**: Cadastro, leitura, atualização e exclusão de vendas.
- **Testes**: Cobertura completa de testes unitários e de integração.
- **Mocks**: Mocks para dependências externas, garantindo testes isolados.
- **Javadocs**: Documentação gerada automaticamente para todas as classes e métodos.

## Como Rodar o Projeto

1. **Clonar o repositório**:

   ```bash
   git clone https://github.com/ewertondrigues/sistema-de-gestao-de-vendas-crud-completo-com-jpa-hibernate-postgre-sql-e-testes-avan-ados.git
   cd project-name
   ```

2. **Configurar o Docker**:

   O projeto usa **Docker** para rodar o banco de dados PostgreSQL. Para iniciar o container do banco, execute:

   ```bash
   docker-compose up -d
   ```

3. **Configurar Banco de Dados**:

   No arquivo `application.properties`, configure as credenciais de acesso ao banco de dados:

   ```properties
   spring.datasource.url=jdbc:postgresql://localhost:5432/mydb
   spring.datasource.username=postgres
   spring.datasource.password=password
   ```

4. **Rodar a Aplicação**:

   Para rodar a aplicação, execute o seguinte comando:

   ```bash
   mvn spring-boot:run
   ```

5. **Executar os Testes**:

   Para rodar os testes unitários e de integração, utilize o comando:

   ```bash
   mvn test
   ```

## Estrutura e Arquitetura

### `Classes Abstratas`

As classes **Cliente**, **Produto** e **Venda** herdam de classes abstratas, facilitando a reutilização de código e mantendo a consistência no modelo de dados.

### `DAO (Data Access Object)`

Cada entidade possui um **DAO** dedicado que abstrai o acesso ao banco de dados, utilizando **JPA** para persistência de dados.

### `Service`

A camada de **Service** contém a lógica de negócios e interage com os DAOs para realizar as operações de CRUD.

### `Interfaces`

Cada classe de serviço e DAO implementa uma interface correspondente. Isso garante flexibilidade e consistência no design do projeto, além de facilitar a extensibilidade.

### Exemplo de Implementação

#### `ClienteService.java`

```java
@Service
public class ClienteService {

    @Autowired
    private ClienteDAO clienteDAO;

    public Cliente criarCliente(Cliente cliente) {
        return clienteDAO.save(cliente);
    }

    public Cliente buscarClientePorId(Long id) {
        return clienteDAO.findById(id).orElseThrow(() -> new EntityNotFoundException("Cliente não encontrado"));
    }

    // Outros métodos de CRUD
}
```

#### `ClienteServiceTest.java` (Testes Unitários)

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class ClienteServiceTest {

    @MockBean
    private ClienteDAO clienteDAO;

    @Autowired
    private ClienteService clienteService;

    @Test
    public void testCriarCliente() {
        Cliente cliente = new Cliente("John", "john@example.com");
        Mockito.when(clienteDAO.save(Mockito.any(Cliente.class))).thenReturn(cliente);

        Cliente resultado = clienteService.criarCliente(cliente);
        assertNotNull(resultado);
        assertEquals("John", resultado.getNome());
    }

    // Testes para outros métodos
}
```

### `Mocking com Mockito`

No exemplo acima, **Mockito** é utilizado para mockar o comportamento do **ClienteDAO** durante os testes, permitindo que o **ClienteService** seja testado de forma isolada.

## Testes

### Testes Unitários

Testes unitários são implementados para verificar o funcionamento correto de cada método nas camadas de serviço e DAO.

### Testes de Integração

Testes de integração são realizados para garantir a interação correta entre as camadas e o banco de dados real ou um banco embutido.

### Mocks

**Mockito** é utilizado para criar mocks de dependências externas durante os testes, permitindo que as unidades sejam testadas de forma independente.

## Documentação Javadoc

A documentação Javadoc está disponível para todas as classes e métodos. Para gerar a documentação, execute o seguinte comando:

```bash
mvn javadoc:javadoc
```

A documentação gerada estará disponível em `target/site/apidocs`.

## Licença

Este projeto está licenciado sob a [MIT License](LICENSE).
```


