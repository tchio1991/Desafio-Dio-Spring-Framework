# Desafio DIO Java Spring Framework 

### Descrição do Desafio

* **Agora é a sua hora de brilhar! Crie uma solução que explore o conceito de Padrões de Projeto na pŕatica. Para isso, você pode reproduzir um dos projetos que criamos durante as aulas ou, caso se sinta preparado, desenvolver uma nova ideia do zero ;-)**

* **Dica: Além dos projetos/repositórios que criamos para este desafio, caso queira explorar novos padrões de projeto digite no Google: “java design patterns github” ou “java design patterns examples”. Com isso, você conhecerá novos padrões e implementações de referência que podem ajudá-lo a dominar esse tema!**

### Spring Framework

**Spring Framework** é um framework desenvolvido para a plataforma **Java** baseado nos padrões de projetos **(Design Patterns)**, inversão de controle e injeção de dependência. É constituído por diversos e completos módulos capazes de dar um boost na aplicação Java.

Antes de aprofundarmos no framework, vamos entender esses importantes Design Patterns em que o Spring Framework é baseado (com exemplos 🙃).

### Inversão de Controle

Inversão de controle (Inversion of Control ou IoC, em inglês) trata-se da **interrupção do fluxo de execução de um código** retirando, de certa forma, o controle sobre ele e delegando-o para uma dependência ou container. O principal propósito é minificar o acoplamento do código.

No Java, falamos mesmo em desacoplamento das classes. Isso permite um ganho enorme em manutenibilidade, além da facilidade de trocar ou acrescentar comportamentos ao sistema, se necessário. Também diminui a possibilidade de ocorrência bugs em cascata.

No Spring Framework, as instâncias das classes são fracamente acopladas, ou seja, a interdependência entre os objetos é mínima.

A inversão de controle, no Spring, é facilitada por outro Design Pattern: Injeção de Dependência.

### Injeção de Dependência

A injeção de dependência tem o propósito de **evitar o acoplamento de código numa aplicação.** Em outras palavras, é a proveniência de instâncias de classes que um objeto precisa sem que este instancie por si mesmo. Podemos dizer que a injeção de dependência é uma forma de aplicar a inversão de controle.

No Spring Framework, podemos fazer a injeção de dependência da seguinte forma:

* anotação @Autowired;
* utilizando o construtor da classe (Constructor Injection);
* utilizando o método setter (Setter Injection).

A anotação @Autowired define um ponto onde a injeção da dependência será realizada. Por exemplo, no código abaixo:

@Service
public class ExampleService {

	@Autowired
	private ExampleRepository exampleRespository;

	// construtor, getters e setters

}

Define-se que uma instância da classe ExampleRepository é uma dependência que será injetada pelo container spring. O Spring gerenciará todo o ciclo de vida dessa dependência em todas as vezes que ExampleService for instanciado.

A utilização de @Autowired como é feita no exemplo acima é conhecida como Field Injection (Injeção de dependência por campo) e, embora seja a mais utilizada, não é a melhor escolha para realizar a injeção.

A injeção por construtor, forma recomendada pela equipe do spring, é como o código abaixo:

@Service
public class ExampleService {

	private ExampleRepository exampleRepository;

	public ExampleService(ExampleRepository exampleRepository) {
		this.exampleRepository = exampleRepository;
	}
}

As vantagens desse modo de injeção são o aumento da legibilidade do código, facilidade de manutenção e facilidade na construção dos testes (O Spring Framework oferece suporte para testes também 😵).

A injeção por método setter:

@Service
public class ExampleService {

	private ExampleRepository exampleRepository;

	@Autowired
	public void setExampleRepository(ExampleRepository                            						              exampleRepository) {

	this.exampleRepository = exampleRepository
	
	}
}
Agora que falamos desses importantes aspectos do Spring Framework, vamos falar de alguns de seus módulos principais e algumas annotations utilizadas. No final, vou mostrar um pequeno tutorial java spring com algumas annotations desses módulos (👏👏👏).

**Obs. 1:** Pode ser que alguma annotation seja de outro módulo, mas isso nada muda.

**Obs. 2:** As annotations abaixo são as principais de cada módulo, mas não se resume a elas.

**Obs. 3:** Parte das annotations precisam ou suportam parâmetros, apesar de não tratarmos desse aspecto. No exemplo que faremos sobre uma aplicação Spring RESTful, isso ficará visível.

### Spring Boot no Spring Framework

O Spring Boot facilita bastante a criação de aplicações Java que utilizam o ecossistema Spring com pouca ou nenhuma configuração para executar o projeto. **Ele abstrai toda a complexidade que uma configuração completa pode trazer** (“just run” 😍).

Esse módulo do Spring Framework foi desenvolvido com base na ideia de convenção sobre configuração. Ou seja, apenas utilizar submódulos necessários sem preocupação com o trabalho de configuração do spring.

Esse módulo do Spring Framework foi desenvolvido com base na ideia de convenção sobre configuração. Ou seja, apenas utilizar submódulos necessários sem preocupação com o trabalho de configuração do spring.

**Algumas anotações utilizadas:**

**@Configuration** – define uma classe como fonte de definições de beans e é uma das anotações essenciais se você estiver usando a configuração baseada em Java.

**@Bean** – utilizada em métodos de uma classe, geralmente marcada com @Configuration, indicando ao Spring Framework que deve invocar aquele método e gerenciar o objeto retornado por ele, ou seja, agora este objeto pode ser injetado em qualquer ponto da sua aplicação (Lembra da injeção de dependência?).

**@Autowired** – já falada e exemplificada, define pontos de injeção de dependências dentro de uma classe.

**@Scope** – define o tempo de vida de um objeto gerenciado pelo Spring Framework. Podemos combinar com outras anotações como @Component ou @Bean.

**@Primary** – é usada quando temos dois métodos anotados com @Bean que retornam o mesmo tipo de objeto. O Spring precisa saber qual deles será injetado por padrão quando for solicitado. Indica qual o deve ser o padrão. 

Obs.: Para alterar o padrão, utiliza-se a annotation @Qualifier.

**@SpringBootApplication** – combina as @Configuration, @EnableAutoConfiguration e @ComponentScan. Desse modo, não precisamos instalar um servidor Web, pois o Spring Boot já vem com um servidor Tomcat incorporado.

 Essa anotação ativa a configuração baseado em Java, bem como o recurso de varredura e configuração automática de componentes do Spring Boot.

**@Profile** – define para qual profile tal bean deve ser carregado. Comum quando existem classes que somente devem ser carregadas em ambiente de desenvolvimento ou de produção ou de teste.

**@EnableAutoConfiguration** –  ativa o recurso de configuração automática.

**@EnableAsync** – quando precisa-se de ações no sistema em background (outra thread). Essa annotation deve ser colocada em classes anotadas com @Configuration, para que o Spring habilite o suporte de execução assíncrona.

**@Async** – habilitado o uso de execução de métodos assíncronos com @EnableAsync, marca-se qualquer método de um bean gerenciado. Assim que tal método é  invocado, o Spring vai garantir que a execução dele será em outra thread.

**@Component** – indica que uma classe vai ser gerenciada pelo container do Spring (Spring Container IoC).

**@ComponentScan** – utilizada em classes de configuração indicando quais pacotes ou classes devem ser escaneadas pelo Spring para que essa configuração funcione.

**@Service** – define uma classe de serviço.

**@RestControllerAdvice** – combinação das annotations @ControllerAdvice e @ResponseBody. Indica ao Spring que se trata de um componente especializado em exceções e que o retorno dos métodos da mesma devem ser inseridos no corpo da resposta HTTP e convertidos para JSON.

**@ControllerAdvice** – lida com exceções num aplicativo Spring MVC. É usada para manipulação global de erros. Tem o controle total sobre o corpo da resposta e código de status.

### Spring Data JPA

O Spring Data tem o propósito de fornecer um modelo de programação baseado em Spring para **acesso a dados de maneira fácil e sem complicações**, mantendo as características especiais do armazenamento de dados subjacente 😮.

Facilita o uso de tecnologias de acesso a dados, banco de dados relacionais e não relacionais, possui características com abstrações de mapeamento e objetos personalizáveis e consultas dinâmicas.

**Algumas anotações utilizadas:**

**@Transactional** – configura o comportamento transacional de um método.

**@NoRepositoryBean** – para que o Spring Framework não crie beans de interface de repositórios comuns para repositórios filhos.

**@Repository** – define um repositório bean (essa não é bem do Spring Data, mas é bem associada a ele)

**@Query** – usada para fornecer uma implementação JPQL para um método de repositório.

**@Param** – definir parâmetros nomeados que serão passados para consultas.

**@Id** – define que o atributo é um identificador.

**@Transient** – marca um campo de uma classe de modelo como transitório. Portanto, o mecanismo de armazenamento de dados não lê ou grava o valor deste campo.

**@GeneratedValue** – define que a geração do id da entidade será gerenciada pelo provedor de persistência (JPA).

### Spring Security no Spring Framework

O Spring Security é uma estrutura de autenticação e autorização poderosa e altamente personalizável para **proteção de aplicações** baseados em Spring Framework.

Concentra-se em fornecer autenticação e autorização para aplicações Java. Para isso, oferece facilidades para extensões e atende toda a personalização de segurança que um projeto Java Spring precisa 😎.

**Algumas anotações utilizadas:**

**@EnableWebSecurity** – habilita recursos de segurança.

**@EnableAuthorizationServer** – habilita o AuthorizationServer.

**@EnableResourceServer** – permite que a aplicação se comporte como um Resource Server.

**@EnableGlobalMethodSecurity** – ativa a segurança de método global.

**@Secured** – é usada para especificar uma lista de funções (papéis) em um método.

**@PreAuthorize** – fornece controle de acesso baseado em expressão.

**@PreFilter** – filtra um argumento de coleção antes de executar o método, definindo regras de segurança refinadas usando o Spring EL. A filtragem é aplicada numa lista que está sendo passada como parâmetro de entrada para o método anotado.

**@PosFilter** – filtra listas de objetos com base nas regras de segurança personalizadas que definimos ou seja, define para filtrar a lista de retorno de um método aplicando essa regra a todos os elementos da lista. 

Se o valor avaliado for verdadeiro, o item será mantido na lista, caso contrário, o item será removido.

**@AuthenticationPrincipal** – indica ao Spring a injeção do usuário logado na aplicação.

### Spring Web e Spring MVC

O Spring Web é utilizado para criar aplicativos Web, incluindo RESTful, utilizando o Spring MVC. Indispensável para criação aplicações web baseadas em Spring Framework.

O Spring MVC é um módulo do spring que ajuda a criar aplicações Web de maneira fácil, simples e elegante, o que possibilita a construção de aplicações web robustas e flexíveis e, como o nome sugere, é baseado no pattern MVC 👀.

No Spring MVC, um controller é criado utilizando a anotação @Controller ou @RestController e para cada método é feita um mapeamento para a URL que o controlador será chamado.

**Algumas anotações utilizadas:**

**@RequestMapping** – mapeia requisições REST.

**@Controller** – define uma classe que contém métodos para estrutura Spring MVC.

**@RestController** – define uma classe que contém métodos para uma API RESTful.

**@RequestBody** – mapeia o corpo da solicitação HTTP para um objeto.

**@PathVariable** – define o recebimento de parâmetros de uma requisição.

**@RequestParam** – com essa anotação, podemos acessar parâmetros da solicitação HTTP.

**@ExcepetionHandler** – lida com exceções. A configuração do Spring detecta essa anotação e registra o método como manipulador de exceções para a classe de exceção do argumento e suas interfaces.

**@ResponseStatus** – com essa anotação, podemos especificar o status HTTP desejado da resposta.

**@ModelAttribute** – define o modelAttribute que será utilizado em um form HTML. Podemos acessar elementos que já estão no modelo de um MVC @Controller favorecendo a chave do modelo.

**@CrossOrigin** – ativa a comunicação entre domínios para os métodos manipuladores de solicitações.

**@SessionAttributes** – declara os atributos da sessão listando os nomes dos atributos do modelo que devem ser armazenados de forma transparente na sessão, servindo como beans de apoio de formulário entre as solicitações subsequentes.

### JPA (Java Persistence API)

Algumas anotações importantes utilizadas numa aplicação Java Spring Framework (essa é uma seção bônus, aproveite!)

**@Entity** – especifica que a classe representa uma entidade no banco de dados. O estado da classe anotada com essa annotation é gerenciado pelo contexto de persistência subjacente.

**@Basic** – mapeia um tipo de atributo básico para uma coluna de uma tabela no banco de dados.

**@Cacheable** – especifica se uma entidade deve ser armazenada no cache de segundo nível.

**@Table** – especifica a tabela da entidade anotada.

**@Column** – especifica o mapeamento entre um atributo básico e a coluna da tabela de banco de dados.

**@Id** – especifica o identificador da entidade. Qualquer entidade precisa ter um atributo identificador, este que é usado ao carregar a entidade em um determinado contexto de persistência.

**@GeneratedValue** – especifica que o valor do identificador de entidade é gerado automaticamente utilizando a coluna de identidade, uma sequência de banco de dados ou um gerador de tabelas.

 O Hibernate (uma implementação da JPA) suporta o mapeamento @GeneratedValue mesmo para os identificadores de UUID.

**@Transient** – especifica que um determinado atributo de entidade não deve ser persistido. Quase a mesma ideia da annotation do Spring Data.

**@Lob** – especifica que o atributo atualmente anotado representa um tipo de objeto grande.

**@OneToOne** – especifica um relacionamento de banco de dados um para um.

**@ManyToOne** – especifica um relacionamento de banco de dados muitos para um.

**@OneToMany** – especifica um relacionamento de banco de dados um para muitos.

**@ManyToMany** – especifica um relacionamento de banco de dados muitos para muitos.

**@JoinColumn** – especifica a coluna FOREIGN KEY utilizada ao ingressar em uma associação de entidades ou em uma coleção incorporável.

**@JoinTable** – especifica a tabela de links entre duas outras tabelas de banco de dados.

**@MapsId** – especifica que o identificador de identidade é mapeado pelo @ManyToOne atualmente anotado ou @OneToOne associado.

**@ElementCollection** – especifica uma coleção de tipos básicos ou incorporáveis.

**@Embeddable** – especifica tipos incorporáveis. Assim como os tipos básicos, os tipos incorporáveis não têm identidade, sendo gerenciados por sua entidade proprietária.

**@Embedded** – especifica que um determinado atributo de entidade representa um tipo incorporável.

**@Enumerated** – especifica que um atributo de entidade representa um tipo enumerado.

**@JoinColumns** – utilizada para agrupar várias anotações @JoinColumn que são utilizadas ao mapear a associação de entidades ou uma coleção incorporável utilizando um identificador composto.

**@NamedQuery** – especifica uma consulta JPQL que pode ser recuperada posteriormente por seu nome.

**@OrderBy** – especifica os atributos da entidade utilizados para classificação ao buscar a coleção atualmente anotada.

**@PersistenceContext** – especifica o EntityManager que precisa ser injetado como dependência.

**@Temporal** – especifica o tipo de tempo do atributo de entidade java.util.Date ou java.util.Calendar.

**@Access** – especifica o tipo de acesso da classe de entidade associada, superclasse associada ou atributo de classe e entidade incorporável.

**@Inheritance** – especifica a estratégia de herança de uma determinada hierarquia de classes de entidade.

**@ForeignKey** – especifica a chave estrangeira associada ao mapeamento @JoinColumn.

**@Mapkey** – especifica a chave de uma associação java.util.Map para o qual o tipo de chave é a chave primária ou atributo da entidade que representa o valor do mapa.

**@NamedQueries** – utilizada para agrupar várias anotações @NamedQuery.

**@PersistenceUnit** – especifica o EntityManagerFactory que precisa ser injetado como dependência.

**@PersistenceUnits** – utilizada para agrupar várias anotações @PersistenceUnit.

**@PostLoad** – especifica um método de retorno de chamada que é acionado depois que uma entidade é carregada.

**@PostPersist** – especifica um método de retorno de chamada que é acionado após uma entidade ser persistida.

**@PostRemove** – especifica um método de retorno de chamada que é acionado após uma entidade ser removida.

**@PostUpdate** – especifica um método de retorno de chamada que é acionado após uma entidade ser atualizada.

**@PrePersist** – especifica um método de retorno de chamada que é acionado antes que uma entidade seja persistida.

**@PreRemove** –  especifica um método de retorno de chamada que é acionado antes que uma entidade seja removida.

**@PreUpdate** –  especifica um método de retorno de chamada que é acionado antes que uma entidade seja atualizada.
