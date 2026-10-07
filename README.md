<div align="center">

# 🏥 VollMed API

**API REST para gestão de médicos e pacientes de uma clínica**

<img src="https://img.shields.io/badge/Java-17-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white" alt="Java 17" />
<img src="https://img.shields.io/badge/Spring%20Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white" alt="Spring Boot" />
<img src="https://img.shields.io/badge/Spring%20Data%20JPA-6DB33F?style=for-the-badge&logo=spring&logoColor=white" alt="Spring Data JPA" />
<img src="https://img.shields.io/badge/Flyway-CC0200?style=for-the-badge&logo=flyway&logoColor=white" alt="Flyway" />
<img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL" />
<img src="https://img.shields.io/badge/Maven-C71A36?style=for-the-badge&logo=apachemaven&logoColor=white" alt="Maven" />

</div>

## 📖 Sobre o projeto

API desenvolvida em **Java com Spring Boot** para cadastrar e gerenciar médicos e pacientes. O projeto foi construído ao longo do curso **Spring Boot 3: desenvolva uma API Rest em Java**, da Alura, aplicando cada conceito na prática.

## ⚙️ Funcionalidades

**Médicos**
- Cadastro com validação dos dados
- Listagem paginada e ordenada por nome, mostrando apenas os médicos ativos
- Atualização de nome, telefone e endereço
- Exclusão lógica: o médico é marcado como inativo e o registro continua no banco

**Pacientes**
- Cadastro com validação dos dados
- Listagem paginada e ordenada por nome
- Atualização de nome, telefone e endereço

## 🔗 Endpoints

| Método | Rota | Descrição |
| --- | --- | --- |
| `POST` | `/medicos` | Cadastra um médico |
| `GET` | `/medicos` | Lista os médicos ativos (paginado) |
| `PUT` | `/medicos` | Atualiza os dados de um médico |
| `DELETE` | `/medicos/{id}` | Inativa um médico (exclusão lógica) |
| `POST` | `/pacientes` | Cadastra um paciente |
| `GET` | `/pacientes` | Lista os pacientes (paginado) |
| `PUT` | `/pacientes` | Atualiza os dados de um paciente |

A paginação aceita os parâmetros padrão do Spring, por exemplo `GET /medicos?size=5&page=1&sort=crm`.

### Exemplo: cadastrar um médico

```json
{
  "nome": "Ana Souza",
  "email": "ana.souza@voll.med",
  "telefone": "11999990000",
  "crm": "123456",
  "especialidade": "CARDIOLOGIA",
  "endereco": {
    "logradouro": "Rua Exemplo",
    "bairro": "Centro",
    "cep": "01001000",
    "cidade": "São Paulo",
    "uf": "SP",
    "numero": "100",
    "complemento": "Sala 2"
  }
}
```

Especialidades aceitas: `ORTOPEDIA`, `CARDIOLOGIA`, `GINECOLOGIA` e `DERMATOLOGIA`.

## 🧱 Conceitos aplicados

- **DTOs com Java Records** para os dados de entrada e de saída da API
- **Enums** para as especialidades médicas
- **Bean Validation** (`@NotBlank`, `@NotNull`, `@Email`, `@Pattern`, `@Valid`) nos dados recebidos
- **Spring Data JPA** com interfaces `JpaRepository`, sem SQL escrito à mão
- **Flyway** para versionar o banco de dados com migrations
- **Paginação e ordenação** com `Pageable`
- **Exclusão lógica** com a coluna `ativo`

## 🗂️ Estrutura

```
api/src/main/java/med/voll/api
├── controller   # MedicoController e PacienteController
├── medico       # entidade, repository, DTOs e enum de especialidade
├── pacientes    # entidade, repository e DTOs
└── endereco     # endereço compartilhado entre médicos e pacientes

api/src/main/resources/db/migration   # migrations do Flyway (V1 a V4)
```

## ▶️ Como rodar

**Pré-requisitos:** Java 17, Maven e MySQL.

1. Clone o repositório e entre na pasta da API:

```bash
git clone https://github.com/RenanCastroAlbuquerque/Crud_Voll_Med_API.git
cd Crud_Voll_Med_API/api
```

2. Crie um banco de dados no MySQL:

```sql
create database vollmed_api;
```

3. Crie o arquivo `src/main/resources/application.properties` (ele não vai para o repositório) com os dados do seu banco:

```properties
spring.datasource.url=jdbc:mysql://localhost/vollmed_api
spring.datasource.username=seu_usuario
spring.datasource.password=sua_senha
```

4. Rode a aplicação:

```bash
./mvnw spring-boot:run
```

O Flyway cria as tabelas na primeira execução, e a API sobe em `http://localhost:8080`. Os endpoints foram testados com o Insomnia.

## 📌 Próximos passos

- [ ] Exclusão lógica também para pacientes
- [ ] Detalhamento de um registro por id
- [ ] Padronizar os retornos com `ResponseEntity` e códigos HTTP
- [ ] Tratamento de erros
- [ ] Autenticação e segurança

---

<div align="center">

Feito por [Renan de Castro Albuquerque](https://www.linkedin.com/in/renan-castro-albuquerque/)

</div>
