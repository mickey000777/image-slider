<template>
<div id="slides" :style="slidesBH">

    <transition-group name="fade" mode="out-in" tag="div" id="slides">
        <div class="slidefoto" :style="achtergrondFoto" 
             :key="images.bron">
            <div class="slideTitel">
                {{images.bijschrift}}
            </div>
        </div>

    </transition-group>

</div>
</template>

<script>

export default {

    data() {
        return {

        }
    },
    props: {
        images: {
            type: Object,
        },
        slideImageBreedte: {
            type: Number,
        },
        slideImageHoogte: {
            type: Number,
        },
        slidesBreedte: {
            type: Number,
        },
        slidesHoogte: {
            type: Number,
        },
        fotoBreedte: {
            type: Number,
        },
        fotoHoogte: {
            type: Number,
        },
    },
    
    computed: {
        achtergrondFoto() {
            return {
                backgroundImage: "url("+this.images.bron+")",
                width: this.slideImageBreedte + "px",
                height: this.slideImageHoogte + "px",
            };
        },
        slidesBH() {
            return {
            backgroundColor: "grey",
            width: this.slidesBreedte + "px",
            height: this.slidesHoogte + "px",
            };
        },
    },
    
}
</script>

<style scoped>
#slides {
    display: flex;
    /*align-items: flex-start;
    justify-content: center;*/
    padding-top: 5px;

}
.slidefoto {
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    display: flex;
    /*align-items: center;*/
}
.slideTitel {
    font-size: 1.05em;
    font-weight: normal;
    color: white;
    display: flex;
    align-self: flex-end;
    margin-bottom: -25px;

}
.fade-enter-active {
    animation-name: fadeenter;
    animation-duration: 1s;
    animation-iteration-count: 1;
}
.fade-move {
    transition: all 1s;
}
.fade-leave-active {
    animation-name: fadeleave;
    animation-duration: 1s;
    animation-iteration-count: 1;
    position: absolute;
}
@keyframes fadeenter {
    from{
        opacity: 0;
    }
    to{
        opacity: 1;
    }
}
@keyframes fadeleave {
    from{
        opacity: 1;
    }
    to{
        opacity: 0;
    }
    
}
</style>
