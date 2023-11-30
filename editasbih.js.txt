$('[data-toggle="tooltip"]').tooltip({
    trigger: 'manual'
 });
document.addEventListener("DOMContentLoaded", function () {
    var clickCount = 0;
    var numDzikir  = 33;
    var mute = 1;
    var style = 1;
    $('[data-toggle="tooltip"]').tooltip('show');
    setTimeout(function(){ $('[data-toggle="tooltip"]').tooltip('hide'); }, 5000);
     /*$("#test").swipe( {
        //Generic swipe handler for all directions
        swipe:function(event, direction, distance, duration, fingerCount, fingerData) {
          $(this).text("You swiped " + direction );  
        },
        //Default is 75px, set to 0 for demo so any distance triggers swipe
         threshold:0
      });*/
    $('#swipe').swipe({
        swipe:function(event, direction, distance, duration, fingerCount, fingerData) {
            // move('.ball').add('margin-left', 200).end();
            Rotate();
            var obj = document.createElement("audio");
            obj.src = './assets/sound/Click.mp3';
            obj.volume = 0.5;
            obj.autoPlay = false;
            obj.preLoad = true;
            obj.controls = true;
            $('.count').html(function(i, val) { return val*1+1 });
            if(mute == 0){
            //obj.load(); 
            }else{
                obj.play();
            }
            getValueDzikir();
            // if(clickCount == 33 || clickCount == 99){
                dzikirCount = clickCount + 1;
            if(dzikirCount == numDzikir){
                var obj2 = document.createElement("audio");
                obj2.src = './assets/sound/Messagenotification.ogg';
                obj2.volume = 0.5;
                obj2.autoPlay = false;
                obj2.preLoad = true;
                obj2.controls = true;
                if(mute == 0){
                //obj.load();
                }else{
                obj2.play();
                }
                
                $.alert({
                    title: 'Alhamdulillah',
                    content: '<p>Kamu sudah berdzikir sebanyak '+dzikirCount+'x.</p><br><strong>Mau lanjut berdzikir...?</strong>',
                    icon: 'far fa-smile',
                    columnClass: 'col-md-5',
                    theme: 'modern',
                    animation: 'scale',
                    type: 'dark',
                    buttons: {
                        buttonA: {
                            text: 'Lanjut',
                            action: function (buttonA) {
                                clickCount++;
                                return true; 
                            }
                        },
                        buttonB: {
                            text: 'Tidak',
                            action: function (buttonB) {
                                $('.count').html(function(i, val) { return val*0 });
                                clickCount=0;
                            }
                        },
                    }
                });
            }else if(clickCount > numDzikir){
                clickCount++;
               
            }
            else{
                clickCount++;
            }
        },threshold:0
    });
    // function play(example, fn) {
    //     $('#example-' + example + ' .play').addEventListener('click', function(e){
    //     e.preventDefault();
    //     fn();
    //     }, false);
    // }
    // play(2, function(){
    //     move('#example-2 .box')
    //     .add('margin-left', 200)
    //     .end();
    // });
    $('#btnReset').click(function() {
        $('.count').html(function(i, val) { return val*0 });
        clickCount=0;
        var obj3 = document.createElement("audio");
        obj3.src = './assets/sound/Messagenotification.ogg';
        obj3.volume = 0.5;
        obj3.autoPlay = false;
        obj3.preLoad = true;
        obj3.controls = true;
        if(mute == 1){
            obj3.play();
        }
    });
    $('#btnCounter').click(function(){
        var obj4 = document.createElement("audio");
        obj4.src = './assets/sound/Messagenotification.ogg';
        obj4.volume = 0.5;
        obj4.autoPlay = false;
        obj4.preLoad = true;
        obj4.controls = true;
        if(clickCount > 0){
            if(mute == 1){
                obj4.play();
            }
            $.alert({
                title: 'Perhatian',
                content: '<p>Mengubah mode saat dzikir berlangsung akan me-reset hitungan yang sedang berjalan.</p><br><strong>Kamu yakin mau mengubah mode dzikir?</strong>',
                icon: 'fa fa-exclamation',
                columnClass: 'col-md-5',
                theme: 'modern',
                animation: 'scale',
                type: 'dark',
                buttons: {
                    buttonA: {
                        text: 'Ya',
                        action: function (buttonA) {
                            $('.count').html(function(i, val) { return val*0 });
                            clickCount=0;
                            changeValueDzikir();
                        }
                    },
                    buttonB: {
                        text: 'Tidak',
                        action: function (buttonB) {
                            return true;
                        }
                    },
                }
            });
        }
        else{
            if(mute == 1){
                obj4.play();
            }
            changeValueDzikir();
        }
    });
    $('#btnMute').click(function() {
        var text = 'Mute';
        // save $(this) so jQuery doesn't have to execute again
        var $this = $(this).find('span');
        if ($this.text() === text) {
            $this.text('Unmute');
        } else {
            $this.text(text)
        }
            if(mute==0){
                mute = 1;
                $('#btnMute').html('<ion-icon name="volume-high"></ion-icon>');
                $('#btnMute').removeClass('active');
            }else{
                mute = 0;
                $('#btnMute').html('<ion-icon name="volume-mute"></ion-icon>');
                $('#btnMute').addClass('active');
            }
    });
    $('#btnStyle').click(function(){
        style++;
        $('body').removeClass();
        $('#box-button').removeClass();
        $('#tasbihNumber').removeClass('contrast');
        if(style == 1){
            // style 1
            // body background
            $('body').addClass('bg1 style1');
            $('#myimage').attr('src', 'assets/img/avatars/ava3.png');
            $('#box-button').addClass('style1');
        }
        else if(style == 2){
            // style 2
            // body background
            $('body').addClass('bg2 style2')
            $('#myimage').attr('src', 'assets/img/avatars/ava4.png');
            $('#box-button').addClass('style2');
        }
        else if(style == 3){
            // style 3
            // body background
            $('body').addClass('bg3 style3')
            $('#myimage').attr('src', 'assets/img/avatars/u_mecca.png');
            $('#tasbihNumber').addClass('contrast');
            $('#box-button').addClass('style3');
        }
        else if(style >= 4){
            // style 2
            // body background
            $('body').addClass('bg4 style4')
            $('#tasbihNumber').addClass('contrast');
            $('#myimage').attr('src', 'assets/img/avatars/ava5.jpg');
            $('#box-button').addClass('style4');
            style = 0;
        }
        // else if(style > 2){
        //     style = 1;
        // }
    });
    function getValueDzikir(){
        numDzikir =  $("#Dzikir").val();
    }
    function changeValueDzikir(){
        getValueDzikir();
        if (numDzikir == 33){
            $('#Dzikir').val('99');
            $('#DzikirCaption').html('99');
        }
        else{
            $('#Dzikir').val('33');
            $('#DzikirCaption').html('33');
        }
    }
    function Rotate(){
        $("#myimage").rotate({
        angle: 0,
        animateTo:360
      })
    }
});