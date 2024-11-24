# POC6-desafio-TechMack
Este projeto é um sistema simples para reservar assentos em um cinema, desenvolvido com React. Ele exibe informações sobre um filme, permite que os usuários escolham assentos disponíveis, calcula o valor total da reserva, e conclui a compra com um alerta de confirmação.
#

## 🚀 Recursos
- Exibição de informações do filme, incluindo título, horário, sinopse, data de lançamento e direção.
- Interface visual para seleção de assentos.
- Assentos disponíveis: Podem ser selecionados.
- Assentos selecionados: São destacados visualmente.
- Assentos indisponíveis: Não podem ser selecionados.
- Cálculo automático do valor total da reserva com base no número de assentos selecionados.
- Botão de confirmação para finalizar a compra e exibir o valor total em um alerta.

## 🛠️ Tecnologias Utilizadas
- React: Biblioteca JavaScript para construir interfaces de usuário.
- CSS Modules: Para estilização modular do projeto.
- JSON: Para armazenar dados fictícios do filme e dos assentos.

## 📂Estrutura do Projeto
- page.module.css: Contém as classes CSS para estilização da página.
- info.json: Contém os dados fictícios do filme e dos assentos.
- Home (arquivo principal): Componente React que gerencia a lógica e exibição da página.

## ⚙️ Como Funciona
 1. Informações do Filme:

- Exibidas no cabeçalho e na descrição lateral direita.
- Dados carregados dinamicamente de um arquivo JSON.
 2. Seleção de Assentos:

- Cada assento é representado por um botão.
- Estados do Assento:
- Disponível: Botão clicável.
- Selecionado: Botão destacado.
- Indisponível: Botão desativado.
- O estado da seleção é gerenciado com o hook useState. 
 3. Cálculo do Total:

- Atualizado automaticamente sempre que um assento é selecionado ou desmarcado.
- Preço por assento: R$25.
 4. Finalizar Compra:

- O botão "Comprar" exibe um alerta com o valor total da compra.

## 📋 Como Usar
1. Clone o repositório ou copie os arquivos para o seu projeto.
2. Certifique-se de que o Node.js está instalado em sua máquina.
3. Instale as dependências:
``` java
npm install
```
4. Inicie o servidor de desenvolvimento:
```java
npm run dev
```
5. Abra o navegador e acesse:
``` java
http://localhost:3000
```
6. Interaja com a página para:
- Selecionar assentos.
- Visualizar o preço total da reserva.
- Finalizar a compra.
#

## 📄 Estrutura do Código
### Hooks e Estados
useState:
- selecionaAssento: Lista de assentos selecionados.
- totalPreco: Valor total calculado com base nos assentos selecionados.

``` java
 const [selecionaAssento, setSelecionaAssento] = useState([]); // Estado para armazenar o preço total
  const [totalPreco, setTotalPreco] = useState(0); // Estado para armazenar o preço total
```
  
useEffect:
- Atualiza totalPreco automaticamente ao alterar selecionaAssento.

``` java
// atualizar o preço total sempre que a lista de assentos selecionados mudar  
  useEffect(() => {
   
    setTotalPreco(selecionaAssento.length * seatPreco); // Calcula o preço total
  }, [selecionaAssento]); // O efeito será executado toda vez que 'selecionaAssento' mudar
```

### Funções Principais
- toggleSeatSelection: Alterna a seleção de um assento.
- exibirCadeiras: Renderiza os botões dos assentos com base nos estados.
- filmeInfo: Exibe o título e horário do filme.
- filmeDesc: Exibe a sinopse, data de lançamento e direção.

``` java
 // Função que alterna a seleção de um assento (seleciona ou desmarca)
  const toggleSeatSelection = (numAssento) => {
    if (selecionaAssento.includes(numAssento)) {
      setSelecionaAssento(selecionaAssento.filter((num) => num !== numAssento));
    } else {
      setSelecionaAssento([...selecionaAssento, numAssento]);
    }
  };

   // Função que exibe as informações básicas do filme (título e horário)
  const filmeInfo = () => (
    <header>
      <h1>{info.titulo}</h1>
      <h2 className={styles.horario}>{info.horario}</h2>
    </header>
  );

   // Função que exibe a descrição do filme (sinopse, data de lançamento, direção)
  const filmeDesc = () => (
    <header className={styles.filmeDesc}>
      <b className="titulo">Sinopse do filme</b>
      <p>{info.sinopse}</p>
      <b>Data de Lançamento</b>
      <p>{info.dataLancamento}</p>
      <b>Direção</b>
      <p>{info.direcao}</p>
    </header>
  );

  // Função que exibe os assentos (disponíveis, selecionados ou indisponíveis)
  const exibirCadeiras = () =>
    info.assentos.map((assento) => {
      const isSelected = selecionaAssento.includes(assento.numero);
      const seatClass = assento.disponivel
        ? isSelected
          ? styles.assentoSelecionado
          : styles.assentoDisponivel
        : styles.assentoIndisponivel;

      return (
        <button
          key={assento.numero}
          className={`${styles.assentos} ${seatClass}`}
          onClick={() => assento.disponivel && toggleSeatSelection(assento.numero)}
          disabled={!assento.disponivel}
        />
      );
    });
```


## 📦 Estrutura de Dados (info.json)
Exemplo de como os dados são estruturados:
``` java

{
  "titulo": "Título do Filme",
  "horario": "20:00",
  "sinopse": "Descrição do filme.",
  "dataLancamento": "2024-01-01",
  "direcao": "Diretor do Filme",
  "assentos": [
    { "numero": 1, "disponivel": true },
    { "numero": 2, "disponivel": false },
    { "numero": 3, "disponivel": true }
  ]
}
```


## 🖼️ Estilização
Os estilos são organizados em módulos CSS:

- Disponível: assentoDisponivel
- Selecionado: assentoSelecionado
- Indisponível: assentoIndisponivel


## ✍️ Autores
- Arthur Eduardo - 10437356
- Felipe Melantonio - 10443843
- Guilherme Sampaio Silva - 10443768
