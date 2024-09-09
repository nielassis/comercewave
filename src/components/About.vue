<template>
    <div class="category-indx">
        <div class="square"></div>
        <p>Sobre</p>
      </div>

   <div class="about">
    <img src="../assets/sapiens.png" alt="" srcset="">
    <div class="desc">
        <p><b>mais do que uma simples plataforma de e-commerce; somos o seu parceiro confiável para uma experiência de compra online excepcional. Fundada com a missão de transformar o modo como você faz compras, nossa empresa combina tecnologia de ponta com um compromisso inabalável com a satisfação do cliente.</b></p>
    </div>
   </div>
</template>

<script>
    export default {
        name: 'AboutUs'
    }
</script>

<style>
    .about {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        text-align: center;

        & img {
            width: 500px;
            height: auto;
        }

        & .desc {
            width: 750px;
            font-size: 16px;
            padding: 50px;
        }
    }
    
 
    .category-indx {
  padding-top: 50px;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  gap: 10px;
  padding-left: 120px;
  padding-bottom: 50px;
}

.square {
  width: 10px;
  height: 30px;
  background-color: #ff6f61;
  border-radius: 8px;
}

.category-indx p {
  color: #ff6f61;
  font-weight: bold;
}


@media (max-width: 480px) {
  .about .desc {
    font-size: 12px;
  }
}
</style>
