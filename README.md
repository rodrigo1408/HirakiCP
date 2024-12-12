
HikariCP é uma biblioteca de pool de conexões para Java, amplamente utilizada em sistemas que utilizam bancos de dados relacionais. Ela é conhecida por sua alta performance, simplicidade e baixa sobrecarga. O pool de conexões é uma técnica que gerencia um conjunto de conexões reutilizáveis ao banco de dados, permitindo maior eficiência ao reduzir o custo de criação e destruição de conexões.

HikariCP é frequentemente integrada com frameworks como Spring Boot e Hibernate para otimizar operações com bancos de dados. Configurações típicas incluem parâmetros como tamanho máximo do pool, tempo limite de conexão, e propriedades específicas do banco de dados para otimizar consultas preparadas e caching.

A partir do Spring Boot 2.0, o HikariCP tornou-se o pool de conexões padrão, devido à sua eficiência em termos de consumo de memória e velocidade. Ele pode ser configurado através de propriedades no arquivo application.properties ou diretamente no código, utilizando classes como HikariConfig e HikariDataSource​.

Se estiver usando Spring Boot, não é necessário incluir manualmente o HikariCP a partir da versão 2.0, pois ele já é o pool padrão, mas caso não esteja utilizando essa versão do spring é necessário adicionar a dependência no pool.xml(para projetos Maven):

    <dependency>
        <groupId>com.zaxxer</groupId>
        <artifactId>HikariCP</artifactId>
        <version>5.0.1</version> <!-- Use a versão mais recente -->
    </dependency>

Configure seu application.properties para esse exemplo

    spring.datasource.url=jdbc:mysql://localhost:3306/seu_banco
    spring.datasource.username=seu_usuario
    spring.datasource.password=sua_senha
    spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
    
    # Configurações específicas do HikariCP 

    logging.level.com.zaxxer.hikari=DEBUG
    logging.level.org.springframework.boot.autoconfigure.jdbc=DEBUG -- log do hirakiCP
    
    spring.datasource.hikari.poolName=SpringBootJPAHikariCP
    spring.datasource.hikari.maximum-pool-size=10
    spring.datasource.hikari.minimum-idle=5
    spring.datasource.hikari.idle-timeout=600000
    spring.datasource.hikari.max-lifetime=1800000
    spring.datasource.hikari.connection-timeout=30000

Se preferir usar o application.yml

    spring:
      datasource:
        url: jdbc:mysql://localhost:3306/seu_banco
        username: seu_usuario
        password: sua_senha
        driver-class-name: com.mysql.cj.jdbc.Driver
        hikari:
          maximum-pool-size: 10
          minimum-idle: 5
          idle-timeout: 300000
          max-lifetime: 900000
          connection-timeout: 20000
          pool-name: SpringBootJPAHikariCP

Se você precisar de configurações avançadas, pode criar uma classe de configuração personalizada, mas isso é opcional.
Segue o link da documentação do mesmo: https://www.baeldung.com/hikaricp
