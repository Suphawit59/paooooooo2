<template>
  <div>
    <h3 class="text-center mt-5">เกมเป่ายิงฉุบ</h3>

    <div class="box-game d-flex justify-content-center mt-5">
      <div class="user1">
        <h5 class="text-center">ผู้เล่น 1</h5>
        <img :src="player1ChoiceImage" alt="">
      </div>

      <div class="user2">
        <h5 class="text-center">ผู้เล่น 2</h5>
        <img :src="player2ChoiceImage" alt="">
      </div>
    </div>

    <div class="button mt-5 d-flex justify-content-center">
      <button class="btn btn-danger" @click="playGame"  data-bs-toggle="modal" data-bs-target="#exampleModal">เกมเป่ายิงฉุบ</button>
      <button @click="Resetgame" class="btn btn-success mx-4">เริ่มใหม่</button>
    </div>
  </div>

  <div class="score mt-3 d-flex justify-content-center">
    <div class="d-flex justify-content-center bg-success p-2 text-dark bg-opacity-25 ">

      <p class="fs-5"> คะแนน {{ scorePlayer1 }} : {{ scorePlayer2 }}</p>
    </div>
</div>




    <!-- Modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h1 class="modal-title fs-5 text-center" id="exampleModalLabel">ผล</h1>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
      <p class="text-center fs-5 fw-bold text-danger">{{ resultMessage }}</p>
      <img :src="imagesplayer" width="250" height="250">
      </div>
     
    </div>
  </div>
</div>

</template>

<script>
export default {
  data() {
    return {
      choices: ['ค้อน', 'กระดาษ', 'กรรไกร'],
      player1Choice: '',
      player2Choice: '',
      player1ChoiceImage: 'https://i.pinimg.com/736x/7c/09/48/7c0948ac69a90aac021fe06632e5a667.jpg  ', // รูปเริ่มต้น
      player2ChoiceImage: 'https://i.pinimg.com/736x/4a/80/47/4a8047b6e20efa3409b9106971c75cdb.jpg', // รูปเริ่มต้น
      resultMessage: '',
      scorePlayer1: 0, // คะแนนผู้เล่น 1
      scorePlayer2: 0,  // คะแนนผู้เล่น 2
      
    };
  },
  methods: {
    playGame() {
      const randomIndex1 = Math.floor(Math.random() * this.choices.length);
      const randomIndex2 = Math.floor(Math.random() * this.choices.length);

      this.player1Choice = this.choices[randomIndex1];
      this.player2Choice = this.choices[randomIndex2];

      this.player1ChoiceImage = this.getImagePath(this.player1Choice);
      this.player2ChoiceImage = this.getImagePath(this.player2Choice);

      this.calculateWinner();
    },
    getImagePath(choice) {
      if (choice === 'ค้อน') {
        return 'https://www.shipshapegroup.com/wp-content/uploads/2017/12/30374.jpg';
      } else if (choice === 'กระดาษ') {
        return 'https://www.thaibook.co.th/wp-content/uploads/2016/06/paper-01.jpg';
      } else if (choice === 'กรรไกร') {
        return 'https://abletoolthailand.com/cdn/shop/products/krraikrtadphaa-taw-stainless-khaaphlaastiktraa-stp-stainless-steel-tailor-shear-stp_580x.jpg?v=1610778556';
      }
    },
    calculateWinner() {
      if (this.player1Choice === this.player2Choice) {
        this.resultMessage = 'เสมอ';
        this.imagesplayer = "https://1.bp.blogspot.com/-mVdk9Ro-aic/Xx_vtfhVkdI/AAAAAAABemc/RczwCDpTlMIDH4qcS3jqh8ydtadZem2swCLcBGAsYHQ/s1600/green-dinosaur.jpg"
      } else if (this.player1Choice ==="ค้อน" && this.player2Choice === "กรรไกร" || 
      this.player1Choice ==="กรรไกร" && this.player2Choice === "กระดาษ" ||
       this.player1Choice ==="กระดาษ" && this.player2Choice === "ค้อน"  ) {
        this.resultMessage = 'ผู้เล่น 1 ชนะ';
        this.scorePlayer1++; // เพิ่มคะแนนผู้เล่น 1
        this.imagesplayer ='https://i.pinimg.com/736x/7c/09/48/7c0948ac69a90aac021fe06632e5a667.jpg';
      } else {
        this.resultMessage = 'ผู้เล่น 2 ชนะ';
        this.scorePlayer2++; // เพิ่มคะแนนผู้เล่น 2
        this.imagesplayer ='https://i.pinimg.com/736x/4a/80/47/4a8047b6e20efa3409b9106971c75cdb.jpg';
        
      }
    },
      Resetgame(){
        window.location.reload(); // รีเซ็ตหน้าเว็บ
      }
    
    }
  
};
</script>

<style>
.user1,.user2{
  border: 2px solid rgb(0, 81, 255);
  padding: 50px;
}
.box-game img{
  width: 250px;
  height: 250px;
}
.user1{
  margin-right: 60px;
}
.modal-body img{
margin-left: 100px;
}
</style>
