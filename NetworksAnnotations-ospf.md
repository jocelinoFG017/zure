Anotações de redes:

Legendas:

   - LSU-> Link State Update.
   
   - LSR-> Link State Request.
   
   - DR - Designed Router.
   
   - DBR - Backup Designed Router.


# Fundamentos OSPF (Open Shorted Path First)
      - É um protocolo de roteamento dinâmico. do tipo link-state(link de estados).
      - Ele se ajusta a melhor rota.
      - Não usa protocolo IP TCP/UDP.
      - Utiliza um protocolo IP próprio type 89.
      - É open source/aberto(FREE).
   
   
   ### OSPF packet types/tipos de pacotes
   
     - Hello -> utilizado para descobrir vizinhos(pacote de aviso).
     - DD -> contem o resumo de toda a tabela topologica.
     - LSR -> requisita um pedido a um vizinho de uma rota especifica.
     - LSU -> o vizinho responde com o LSA completo, entrega a rota(a melhor rota no caso).
     - LSAck -> confirma que recebeu a rota especifica ou algum pacote ospf(pacotes hello não necessitam confirmação).
     
   
   ### Routers types
      - DR -> o maior IP/ todos fazem adjacencia com ele/ é como se fosse o sindico.
      - BDR -> o segundo maior IP/ é como se fosse o sub-sindico. o backup em caso de falha do DR
      - Internal router -> somente em uma area e não pode estar na area 0.
      - Backbone router -> Somente na area 0.
      - ABR -> é responsável por conectar duas ou mais áreas.
      - ASBR -> conecta outros protocolos de roteamento ( redistribuição ) para dentro do protocolo OSPF.
      

TABELA TOPOLOGICA (todas as rotas, all routers)
   - Contem toda a rede/TODAS AS ROTAS.
   
TABELA DE ROTEAMENTO
  - Contem só as melhores rotas.

TABELA DE VIZINHANÇA
  - se tudo estiver certo ele forma uma adjacencia construindo uma tabela de vizinhança.
  - contem os endereços mais pertos.

# Configurações no Roteador


1 - intra-area(O) - é usado quando a origem  e o destino estão na mesma area.

2 - inter-area(O IA) - quando estão em areas diferentes.

wild card mask- > aonde eu tenho 0 é fixo. onde não tem pode ser qualquer numero.

exemplo 1: 192.168.30.1 0.0.0.255

192 obrigatorio

.168 obrigatorio

.30 obrigatorio

.1 pode ser qualquer numero



## Comandos

 - router ospf ? (o ? pode ser um numero)

 - network < ip and wild card mask>

 - ena = enable

 - conf t = configure terminal

 - int = interface

 - show ip ospf neighbor    -> tabela de vizinhança

 - show ip route         -> tabela de roteamento

 - show ip ospf database -> tabela topologica


---------- CONFIGURANDO OSPF ---

### PASSO 01 - Adicionando um ip a uma porta e ativando-a

1º * ena

2º * conf t

3º * int (porta(ex: int f0/0))

4º * ip address 192....(ex:192.168.0.2 255.255.255.0)   ** endereço ip + a maskara

5º * no shut

6º * exit

#### Atenção primeiro tem que adicionar um ip a entrada(porta(ou seja faça isso antes de ir configurar o OSPF no roteador)).(VER passo 01)
  ------- Agora o vem o ospf --------
### PASSO 02 - Configurando o OSPF no roteador
  
1º * router ospf ?(?->pode ser qualquer NUMERO, ou você pode simplesmente deixar o (?))

2º * network 192.168.x.x 0.0.0.255 area 0     

*(x == ao IP de sua preferencia)*(0.0.0.255 == mascara coringa)(area -> tem que ter uma area se não, não vai dar certo)

3º * no shut(talvez não seja necessário esse aqui, mas na duvida de um no shut aqui tambem).

4º * exit

5º * wr (pra salvar as alterações feitas no roteador).

### Observações
OBS01: ignore as *(estrelinhas)

se você estiver usando o packet tracer terá de fazer todos os passos no segundo roteador conectando-os na mesma area, se tudo estiver correto acontecerá a adjacencia entre os roteadores.


### Links youtube uteis:
https://www.youtube.com/watch?v=a-jDa3vTUfA
