<h1 align="center"> Docker Lab para Iniciantes </h1>
	
	Nesse repositório, irei abordar conceitos inicias de Docker e tutoriais para iniciantes que queiram entender melhor o funcionamento dessa ferramenta, veremos também configurações de serviços DNS, Proxy Reverso e um pouco de manipulação de redes.

#O que é o Docker e por que usamos?
	Para entender o Docker, precisamos entender o problema que ele resolveu. Antigamente, o maior pesadelo de um desevolvedor era a frase: "Mas na minha máquina funciona!". Isso acontecia pelo simples fato de que o ambiente do desenvolver era diferente do ambiente de produção.
	O Docker surgiu para "empacotar" sua aplicação e todas as suas dependências em uma unidade padronizada chamada Container.
	
#O conceito de Container

	Vamos imaginar o seguinte, nós temos um navio com um container com diversos conteúdos dentro, sejam eletrônicos, café, camisas, ou o que for. Quando o guindaste vem para mover esses containeres, ele sabe exatamente como fazer isso, porque o exterior é padronizado.
	O Docker faz o mesmo com o software: ele garante que o sistema rode da mesma forma em qualquer lugar (No seu computador, na nuvem, servidor, etc.).
	
#Docker vs. Máquinas Virtuais(VMs)
	Uma dúvida muito comum das pessoas é de que esse tipo de formato é parecido com máquinas virtuais, mas a resposta curta e direta é simplesmente: não, são ferramentas diferentes para ocasiões diferentes, vamos ver  
     Característica         Máquinas Virtuais(VMs)                Docker(Containeres)
	
	Peso                Pesadas - Cada uma tem um SO           Leves - Compartilham o Kernel do Hospedeiro
			    (Sistema Operacional)
	Velocidade	   Lentas - Minutos para dar boot	   Instantâneas - Poucos segundos para subir
	
	Recursos	   Reservam RAM e CPU fixos                Usam apenas o necessário conforme a demanda

	Isolamento	   Isolamento total ao nível de Hardware   Isolamento ao nível de Processo

	Por que o Docker ganha?


#Configurações Iniciais de um Sistema com Docker


	Inicialmente, precisamos instalar o docker e suas pendências para que possamos dar procedimento.

	Siga, a seguir, a documentação oficial do Docker para instalação:  https://docs.docker.com/engine/install/  (Escolha o seu sistema e siga as instruções, caso queira instalar o Docker Desktop, fique a vontade)





#Como o Docker gerencia tudo isso, afinal?
	Para iniciarmos a explicação, eu gostaria de falar um pouco sobre como o Docker funciona por dentro, e basicamente ele trabalha em 3 pilares principais, os quais você verá nesse projeto.

1. Isolamento de Processos

	Basicamente, quando o Docker lê a imagem de um serviço (image: adguard/adguardhome), ele baixa arquivos que contém apenas o necessário para essa aplicação funcionar () 
