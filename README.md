# Aplicação de chats e API

Este projeto foi feito com o intuito de comprovar meus aprendizados sobre API, as formas possíveis de se auxiliar a partir de um assistente IA. A seguir, apresentarei os conceitos e macetes aprendidos ao longo do curso.


### Principais funções

- chat
- Completar
- imagens
- Áudio

#### O modo para configurar cada função pode diferir um pouco de um modelo para outro, MAS, todas seguem o mesmo princípio.

 Defina suas atividades com clareza, contexto aplicado da sua ideia, objetivo do prompt e o formato que vai utilizar, ou seja, os shots

 Zero-shot:
- sem exemplos
- respostas diretas e sem bifurcações no raciocínio
- baseado APENAS no prompt
- Não possui muita capacidade para formatar a partir da adição de exemplos novos

One-shot:
- Utiliza exemplos
- Resposta ampla 
- Baseia-se no prompt e, também, em outras fontes
- Pode ser formatado com mais facilidade a partir da adição de exemplos

Few-Shot 

- Dá vários exemplos de respostas
- Auxilia a ver comportamentos diferentes para uma mesma situação

 ### Como chamar o objeto na hora de codar?

 client = AzureOpenAI(
  azure_endpoint = os.getenv("AZURE_OPENAI_ENDPOINT"), 
  api_key=os.getenv("AZURE_OPENAI_API_KEY"),  
  api_version="2025-04-06"
)

#### Função complete

HTTP:

ex1: Formula uma conclusão ao prompt parâmetros e modelo utilizados 
{
 "prompt": [
  "give me a really short story of a funny student"
 ],
 "max_tokens": 32,
 "temperature": 1.0,
 "n": 1
}

#### Função Chat 

client.chat.completions.create(
            model=os.getenv("AZURE_OPENAI_DEPLOYMENT_NAME"),
            messages=messages,
            temperature=0.7
        )


#### Função imagem

response = client.images.generate(
                model="dall-e-3",  # ou seu modelo configurado
                prompt=prompt,
                n=1,
                size="1024x1024" ou alguma outra medida que preferir
            )

##### Criar boas imagens usando o Dall-E 

para gerar imagens condizentes com a ideia inicial, alguns passo a passos devem ser obecidos. 
1) O prompt deve ter clareza e especificidade
2) O contexto da imagem idealizada deve ser bem detalhado
3) O prompt precisa de uma estrutura concisa

OBS: utilizar o Dall-E SOMENTE para prototipar coisas, é muito fácil identificar algo feito por IA

### variáveis mais comuns

- Temperature
- Top-P
- Tokens máximos
- Penalidades 
- ID do modelo 

#### Top-P x Temperatura

Temperatura: Pega um número x de palavras e Controla quão aleatório são as ligações 

Temperatura 0: Respostas previsíveis e deterministas
Temperatura 1: Respostasmuito improváveis, a maioria sem sentido

Top-P: Controla quais palavras podem ser usadas na possível escolha, ou seja, filtra as opções escolhidas pela tempetratura

Top-P 0.1: só considera o primeiro grupo de palavras até dar o eixo de 10% das possibilidades

Top-P 0.9: considera palavras até dar o eixo de 90% das possibilidades

##### Obs:

Top-P alto + Temperatura alta = criatividade máxima
Top-P alto + Temperatura baixa = variedade controlada
Top-P baixo + Temperatura alta = criatividade limitada
Top-p baixo + Temperatura baixa = máxima previsibilidade

como são alterações bruscas, altere Top-P OU Temperatura. Raramente será bom alterar os dois simultaneamente.

#### Frequency/Presency

Frequency Penalty: defini quanto o algorítmo punirá a repetição de tokens

Presency Penalty: penalidade por diversidade temática


Para fazer o deploy desse projeto, verifique se você possui o acesso de Admin OU se tem acesso o suficiente para lançar o recurso OpenAI no Azure

Após isso, será possível acessar o Playground, uma UI facilitada com o intuito de explorar os recursos. Os recursos são o desenvolvimento de prompt e o preparo de modelos especializados a alguma função.

obs: o mesmo prompt pode ter resultados diferentes, pois modelos de linguagem são estocásticos

### Tokenização

para configurar os tokens, é preferível que se utilize da língua inglesa. Isso, uma vez que o português consome mais tokens que o inglês na maioria dos casos. Ademais, a ferramenta usada para converter Tokens é a [TikToken](https://platform.openai.com/tokenizer) 

## Informações necessárias

O API do Azure é bem configurado e é possível ver como foi feito

Max Completion ≠ max tokens

Max Completion tokens: quantos tokens eu posso gerar para finalizar o chat

API: forma que sistemas interagem entre si a fim de trocar informações sem dar problema

Codex não é mais necessário 

 Para SUA segurança: jamais, EM HIPÓTESE ALGUMA, mande dados pessoais que sejam sensíveis como: dados bancários

###Aprofundamento leve sobre o funcionamento das APIs:

As APIs funcionam como intermediárias, permitindo que um software acesse os recursos e funcionalidades de outro. Elas fornecem uma maneira padronizada para solicitar e receber dados, executar operações e integrar sistemas diversos.

No contexto da programação, as APIs são criadas com base em requisições HTTP (Hypertext Transfer Protocol) que enviam solicitações para um servidor. As requisições geralmente incluem métodos como GET, POST, PUT e DELETE para especificar a ação desejada. Por exemplo, ao utilizar uma API de previsão do tempo, uma aplicação pode enviar uma requisição GET para obter os dados meteorológicos atuais.

Além disso, as APIs utilizam formatos de dados como JSON (JavaScript Object Notation) ou XML (eXtensible Markup Language) para estruturar as informações transmitidas. O JSON é amplamente utilizado devido à sua simplicidade e facilidade de leitura por pessoas e máquinas.


## Referência

 - [Bootcamp DIO: Microsoft AI for Tech - OpenAI Services](https://web.dio.me/track/microsoft-azure-open-ai)

- [Azure OpenAI Service REST API reference](https://learn.microsoft.com/en-us/azure/ai-services/openai/reference)
