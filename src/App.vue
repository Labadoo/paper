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
      player1ChoiceImage: 'https://i.pinimg.com/originals/54/bc/d3/54bcd3702324c3d419220f6e203e2a80.jpg  ', // รูปเริ่มต้น
      player2ChoiceImage: 'https://i.pinimg.com/originals/39/16/ad/3916adc75f89a5186f5da918da0357df.jpg', // รูปเริ่มต้น
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
        return 'https://i.pinimg.com/736x/c5/ff/dd/c5ffddec81527a112a48d168e7dfea01.jpg';
      } else if (choice === 'กระดาษ') {
        return 'https://i.pinimg.com/originals/4c/ab/89/4cab89c1724da313430bb4653f72a1d1.jpg';
      } else if (choice === 'กรรไกร') {
        return 'https://i.pinimg.com/originals/98/53/e7/9853e7e44b17d70d433f551bd9ac2768.png';
      }
    },
    calculateWinner() {
      if (this.player1Choice === this.player2Choice) {
        this.resultMessage = 'เสมอ';
        this.imagesplayer = "https://i.pinimg.com/originals/4c/51/a0/4c51a0b59588e94da486e9997abe1872.jpg"
      } else if (this.player1Choice ==="ค้อน" && this.player2Choice === "กรรไกร" || 
      this.player1Choice ==="กรรไกร" && this.player2Choice === "กระดาษ" ||
       this.player1Choice ==="กระดาษ" && this.player2Choice === "ค้อน"  ) {
        this.resultMessage = 'ผู้เล่น 1 ชนะ';
        this.scorePlayer1++; // เพิ่มคะแนนผู้เล่น 1
        this.imagesplayer ='https://i.pinimg.com/originals/54/bc/d3/54bcd3702324c3d419220f6e203e2a80.jpg';
      } else {
        this.resultMessage = 'ผู้เล่น 2 ชนะ';
        this.scorePlayer2++; // เพิ่มคะแนนผู้เล่น 2
        this.imagesplayer ='https://i.pinimg.com/originals/39/16/ad/3916adc75f89a5186f5da918da0357df.jpg';
        
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
  border: 2px solid black;
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
