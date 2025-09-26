# Loop Challenge - Guia de Implementação

## Objetivo
Neste desafio, você deverá criar um script em Python que realize requisições HTTP em intervalos específicos de tempo. O desafio testa sua capacidade de trabalhar com loops, requisições HTTP, autenticação e temporização precisa.

## Pré-requisitos
- Reutilize o código de autenticação da aula anterior
- Familiaridade com requisições HTTP em Python
- Compreensão de manipulação de tempo em programação

## Estrutura da API

### Endpoint do Desafio
- URL: `/challenges/loop`
- Método: POST
- Headers necessários: 
  - `Authorization: Bearer seu-token`
- Body da requisição:
  ```json
  {
    "maxIterations": numero_maximo_de_iteracoes
  }
  ```

### Possíveis Status de Retorno

1. **START** - Início do Desafio
   ```json
   {
     "status": "START",
     "message": "Desafio iniciado! Você precisa fazer X requisições. A próxima deve ser em Y segundos.",
     "nextWaitTimeInSeconds": Y,
     "progress": "1 / X"
   }
   ```

2. **CONTINUE** - Continuar Desafio
   ```json
   {
     "status": "CONTINUE",
     "message": "Correto! Próxima requisição em Y segundos.",
     "nextWaitTimeInSeconds": Y,
     "progress": "N / X"
   }
   ```

3. **SUCCESS** - Desafio Concluído
   ```json
   {
     "status": "SUCCESS",
     "message": "Parabéns! Você completou o desafio de loop com sucesso!"
   }
   ```

4. **TOO_EARLY** - Requisição Antecipada
   ```json
   {
     "status": "TOO_EARLY",
     "message": "Requisição muito cedo! Desafio resetado."
   }
   ```

5. **TOO_LATE** - Requisição Atrasada
   ```json
   {
     "status": "TOO_LATE",
     "message": "Requisição muito tarde! Desafio resetado."
   }
   ```

## Regras do Desafio

1. **Início do Desafio**
   - Faça uma requisição inicial especificando o número máximo de iterações desejado
   - O servidor determinará aleatoriamente um número de iterações entre 2 e o máximo solicitado
   - Você receberá o tempo de espera para a próxima requisição

2. **Requisições Subsequentes**
   - Cada resposta bem-sucedida incluirá:
     - Status atual do desafio
     - Tempo de espera para a próxima requisição
     - Progresso atual (ex: "2 / 5")
     - Mensagem informativa

3. **Temporização**
   - O servidor fornece o tempo exato de espera em segundos
   - O tempo de espera varia entre 5 e 60 segundos

4. **Condições de Falha**
   - Requisição muito antecipada (antes do tempo especificado)
   - Requisição muito atrasada (após o tempo especificado)
   - Em caso de falha, o desafio é resetado automaticamente

## Dicas para Implementação

1. **Antes de Começar**
   - Teste o fluxo completo usando Postman ou Insomnia
   - Entenda os diferentes status de retorno
   - Planeje como vai lidar com a temporização

2. **Durante o Desenvolvimento**
   - Considere a latência da rede em seu cálculo de tempo
   - Implemente logs para debug
   - Trate possíveis erros de conexão

3. **Pontos de Atenção**
   - A precisão da temporização é crucial
   - Mantenha uma conexão estável
   - Monitore os status de retorno
   - Implemente tratamento de erros adequado

## Sugestões de Melhoria

Depois de conseguir uma implementação básica funcionando, considere adicionar:
1. Sistema de retry para falhas de rede
2. Compensação automática de latência
3. Sistema de logging detalhado
4. Interface de linha de comando com opções configuráveis

Boa sorte!
