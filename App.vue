<style scoped>
  /* Estilos Gerais */

  /* Barra de navegação */
  .navbar {
    display: flex;
    justify-content: center;
    background-color: #2A9D8F;
    padding: 2rem;
    font-size:1.5rem ;/* aumente este valor para ajustar o tamanho da letra */
  }

  .navbar a {
    color: white;
    text-decoration: none;
    margin: 0 1rem;
    font-weight: bold;
    transition: color 0.3s;
  }

  .navbar a:hover {
    color: #FFD700;
  }

  /* Cabeçalho */
  .header {
    text-align: center;
    color: white;
    padding: 20rem 8rem;
    background-image: url('https://emalgumlugardomundo.com.br/wp-content/uploads/2023/05/delta-do-parnaiba-piaui-praia-da-pedra-do-sal.jpg');
    background-size: cover;
    background-position: center;
    position: relative;
  }

  .header::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.4); /* Aumenta a opacidade para 0.8 para escurecer mais */
}



  .header-content {
    position: relative;
    z-index: 1;
  }

  .header h1 {
    font-size: 3rem;
    font-weight: bold;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
    color: #FFD700;
  }

  .header p {
    font-size: 1.4rem;
    margin-top: 0.5rem;
    color: #FFEBCD;
  }

  /* Estilos para a seção de cartões */
  .card-section {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    margin: 2rem;
    gap: 1rem;
  }

  /* Responsividade para os cartões */
  @media (max-width: 600px) {
    .card {
      flex: 1 1 100%;
    }
  }

  @media (max-width: 900px) {
    .card {
      flex: 1 1 48%;
    }
  }

  @media (min-width: 901px) {
    .card {
      flex: 1 1 30%;
    }
  }

  /* Estilos específicos dos cartões */
  .card {
    background-color: #FFF8DC;
    border-radius: 10px;
    box-shadow: 0 6px 12px rgba(0, 0, 0, 0.3);
    overflow: hidden;
    text-align: center;
    transition: transform 0.3s, box-shadow 0.3s;
    flex: 1 1 30%;
    margin: 0 1rem;
  }

  .card:hover {
    transform: scale(1.05);
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.4);
  }

  .card img {
    width: 100%;
    height: 200px; /* Define uma altura fixa */
    object-fit: cover; /* Garante que a imagem não distorça */
  }

  .card h3 {
    color: #2A9D8F;
    margin: 1rem 0;
    font-size: 1.5rem;
    font-weight: bold;
  }

  .card p {
    padding: 0 1rem;
    color: #555;
  }

  .card button {
    margin: 1rem 0;
    padding: 0.5rem 1rem;
    background-color: #E76F51;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s;
  }

  .card button:hover {
    background-color: #D45732;
  }

  /* Descrição expandida */
  .descricao-expandida {
    padding: 1rem;
    background-color: #FFFAF0;
    color: #333;
    font-size: 0.9rem;
  }
</style>

<template>
  <div id="app">
    <!-- Barra de navegação -->
    <nav class="navbar">
      <a href="#" @click="mostrarSecao('pontosTuristicos')">Pontos Turísticos</a>
      <a href="#" @click="mostrarSecao('eventos')">Eventos</a>
      <a href="#" @click="mostrarSecao('hospedagem')">Hospedagem</a>
      <a href="#" @click="mostrarSecao('gastronomia')">Gastronomia</a>
    </nav>

    <!-- Cabeçalho com saudação e imagem de fundo -->
    <header class="header">
      <div class="header-content">
        <h1>Bem-vindo a Parnaíba!</h1>
        <p>Descubra a beleza e cultura dessa cidade incrível.</p>
      </div>
    </header>

    <!-- Seção dinâmica de conteúdo -->
    <section v-if="secaoAtiva" class="card-section">
      <div v-for="(item, index) in conteudoSecaoAtiva" :key="index" class="card">
        <img :src="item.imagem" :alt="item.titulo">
        <h3>{{ item.titulo }}</h3>
        <p>{{ item.descricao }}</p>
        <button @click="mostrarMais(index)">Ver Mais</button>
        <div v-if="item.expandido" class="descricao-expandida">
          <p>{{ item.detalhes }}</p>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      secaoAtiva: '',
      pontosTuristicos: [
        {
          titulo: 'Praia da Pedra do Sal',
          descricao: 'Uma praia de beleza única com formações rochosas.',
          imagem: 'https://conhecaparnaiba.com/wp-content/uploads/2023/01/Rocha-pedra-do-sal--1024x576.jpg',
          detalhes: 'A Praia da Pedra do Sal é famosa por suas pedras e beleza natural.',
          expandido: false
        },
        {
          titulo: 'Delta do Parnaíba',
          descricao: 'O único delta das Américas em mar aberto, é o maior delta em mar aberto das Américas e o terceiro maior do mundo.',
          imagem: 'https://emalgumlugardomundo.com.br/wp-content/uploads/2023/05/delta-do-parnaiba-piaui-ilha-melanceiras.jpg',
          detalhes: 'O Delta do Parnaíba oferece passeios incríveis e contato com a natureza.',
          expandido: false
        },
        {
          titulo: 'Porto das Barcas',
          descricao: 'Centro histórico com construções do período colonial.',
          imagem: 'https://deltarioparnaiba.com.br/wp-content/uploads/2017/10/porto-das-barcas-parnaiba-e1521924007322.jpg',
          detalhes: 'O Porto das Barcas é um marco histórico, repleto de cultura e história.',
          expandido: false
        }
      ],
      eventos: [
        {
          titulo: 'Festival de verão de parnaiba',
          descricao: 'Festival de Verão em Parnaíba, Piauí.',
          imagem: 'https://turismo.pi.gov.br/wp-content/uploads/2024/09/IMG_7950_0da1fc497a.jpeg',
          detalhes: 'Evento cultural com música, dança e turismo.',
          expandido: false
        },
        {
          titulo: ' São João da Parnaíba',
          descricao: 'O evento é considerado o maior São João do estado',
          imagem: 'https://s2.glbimg.com/VHp_6UDWFQhDGpbw0VrXUZRwExk=/620x465/s.glbimg.com/jo/g1/f/original/2014/07/06/quadrilha_phb.jpg',
          detalhes: 'É um evento cultural tradicional que acontece na Praça de Eventos Mandu Ladino, em Parnaíba, Piauí.',
          expandido: false
        },
        {
          titulo: 'Feira de artesanato do porto das barcas',
          descricao: 'Exposição de produtos artesanais locais.',
          imagem: 'https://viajento.com/wp-content/uploads/2022/07/porto-das-barcas-parnaiba-piaui-brasil-loja.jpg?w=1024',
          detalhes: 'Realizada no Porto das Barcas, com peças únicas que destacam a cultura regional​​.',
          expandido: false
        }
      ],
      hospedagem: [
        {
          titulo: 'Hotel arrey',
          descricao: 'Conforto, boa localização e excelente atendimento',
          imagem: 'https://cf.bstatic.com/xdata/images/hotel/max1024x768/86939880.jpg?k=0a99a8f2499e321fcf898ccac368c38fc66cd18ff3002c562d92424730d64268&o=&hp=1',
          detalhes: 'O Hotel Arrey em Parnaíba oferece acomodações confortáveis e atendimento de qualidade. Ideal para quem busca um lugar tranquilo, com boa localização e fácil acesso às principais atrações da cidade.',
          expandido: false
        },
        {
          titulo: 'Pousada vila cajuina',
          descricao: 'Acomodações confortáveis com ambiente familiar.',
          imagem: 'https://cf.bstatic.com/xdata/images/hotel/max1024x768/299871508.jpg?k=e9860f2bfea96f817dd5e3774681253e9a87b0600863707073c28b530bf01cec&o=&hp=1',
          detalhes: 'Localização central, estacionamento gratuito, Wi-Fi e proximidade de atrações turísticas.',
          expandido: false
        },
        {
          titulo: 'Resort Delta',
          descricao: 'Luxo e comodidade para aproveitar o melhor de Parnaíba.',
          imagem: 'https://www.ilhadospoldros.com.br/images/slides/slide2_ilhadospoldros_pousada.jpg',
          detalhes: 'O Resort Delta oferece uma experiência de luxo e contato com a natureza.',
          expandido: false
        }
      ],
      gastronomia: [
        {
          titulo: 'Picanharia 23',
          descricao: ' Rodízio de carnes e buffet variado, ambiente aconchegante.',
          imagem: 'https://media-cdn.tripadvisor.com/media/photo-s/18/f9/ad/a9/venha-experimentar-a.jpg',
          detalhes: 'A Churrascaria 23 em Parnaíba é famosa pelo rodízio de carnes saborosas e um buffet variado, com pratos típicos brasileiros. Ambiente simples e aconchegante.',
          expandido: false
        },
        {
          titulo: 'Restaurante Mangatá',
          descricao: 'Uma experiência gastronômica única e autêntica.',
          imagem: 'https://lh3.googleusercontent.com/p/AF1QipMbSbck4i15JCrOs2NuB6_dHS3zc1z-nBbXyu3S=s1360-w1360-h1020',
          detalhes: 'O Mangatá é um restaurante de frutos do mar em Parnaíba, com ambiente aconchegante e pratos regionais deliciosos, como moqueca e bobó de camarão.',
          expandido: false
        },
        {
          titulo: 'Restaurante Don Ladino',
          descricao: 'Culinária italiana e massas artesanais.',
          imagem: 'https://dynamic-media-cdn.tripadvisor.com/media/photo-o/21/f5/90/da/ambiente-externo.jpg?w=1200&h=-1&s=1',
          detalhes: 'O Don Ladino é um restaurante italiano em Parnaíba, famoso por suas massas artesanais e pizzas em um ambiente acolhedor.',
          expandido: false
        }
      ]
    };
  },
  computed: {
    conteudoSecaoAtiva() {
      switch (this.secaoAtiva) {
        case 'pontosTuristicos':
          return this.pontosTuristicos;
        case 'eventos':
          return this.eventos;
        case 'hospedagem':
          return this.hospedagem;
        case 'gastronomia':
          return this.gastronomia;
        default:
          return [];
      }
    }
  },
  methods: {
    mostrarSecao(secao) {
      this.secaoAtiva = secao;
    },
    mostrarMais(index) {
      const secao = this.conteudoSecaoAtiva;
      secao[index].expandido = !secao[index].expandido;
    }
  }
};
</script>