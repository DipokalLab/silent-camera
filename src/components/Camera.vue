
<template>
  <header class="text-center">
    <div class="relative text-gray-800 h-full">
        <video ref="camera" class="absolute bg-black h-full" :width="1080" :height="1920" autoplay playsinline muted></video>

        <div class="block fixed inset-x-0 bottom-0 pb-10 mx-3">
            <div class="flex items-center">
                <div class="flex-none w-14 h-14 ">
                    
                </div>
                <div class="grow z-20">
                    <button type="button" @click="takePicture" class="text-white bg-slate-700 hover:bg-slate-800 font-medium rounded-md text-sm px-4 py-4 dark:bg-slate-600 dark:hover:bg-slate-700 focus:outline-none dark:focus:ring-blue-800" data-bs-toggle="modal" data-bs-target="#exampleModal">
                        <span class="material-icons-outlined w-8 h-8 text-2xl">
                        photo_camera
                        </span>
                    </button>
                </div>
                <div class="flex-none w-14 h-14 ">
                    <button type="button" @click="toggleCamera" class="text-white  bg-slate-800 hover:bg-slate-900 font-medium rounded-full text-sm px-3 py-3 dark:bg-slate-800 dark:hover:bg-slate-900 focus:outline-none dark:focus:ring-blue-800" data-bs-toggle="modal" data-bs-target="#exampleModal">
                        <span class="material-icons-outlined w-8 h-8 text-2xl">
                        autorenew
                        </span>
                    </button>
                </div>
            </div>


 
        </div>


  <div v-if="isModalVisible" class="absolute shadow-lg w-full h-full flex bg-black bg-opacity-70 justify-center align-middle items-center z-10">
      <div class="w-2/3 p-4 bg-white rounded-md relative">
        <div class="relative w-full">
            <div class="flex text-center items-center justify-center pb-3">
                <h1 class="font-bold text-2xl">사진 미리보기</h1>
            </div>
        </div>
        <div class="w-full">
        
            <img src="" ref="image" class="rounded-md" alt="">

        </div>
        <div class="w-full">
            <button
                @click="isModalOpen = false" 
                class="block bottom-0 right-0 bg-red-100 text-red-600 rounded-md w-full h-10 mt-3  hover:text-red-600 hover:bg-red-200" >
                닫기
            </button>
        </div>
      </div>
  </div>

    </div>
    <canvas ref="canvas" :width="1920" :height="1080" class=" d-none"></canvas>


  </header>
</template>


<script>
    export default {
        data() {
            return {
                isCameraOpen: false,
                isModalOpen: false,
                videoStream: undefined,
                videoConstraints: {
                    audio: false,
                    video: {
                        width: 1920,
                        height: 1080,
                        facingMode: "environment"
                    }
                    
                },
            }
        },
    
        methods: {
            onWindowLoad() {
                this.openCamera()
            },
            takePicture() {
                this.isModalOpen = true

                const video = this.$refs.camera
                const canvas = this.$refs.canvas
                canvas.width = video.videoWidth
                canvas.height = video.videoHeight
                const ctx = canvas.getContext("2d")

                const videoSize = {
                    w: video.videoWidth,
                    h: video.videoHeight
                }
                ctx.drawImage(video, 0, 0, videoSize.w, videoSize.h)
                this.canvasToImage()
            },
            canvasToImage() {
                const canvas = this.$refs.canvas

                canvas.toBlob((blob) => {
                    const image = this.$refs.image
                    const url = URL.createObjectURL(blob);

                    image.onload = () => {
                        URL.revokeObjectURL(url);

                    };
                    image.src = url;


                });
            },
            toggleCamera() {
                this.videoConstraints.video.facingMode = this.videoConstraints.video.facingMode == "user" ? "environment" : "user"
                this.loadCamera()
            },
            openCamera() {
                if (!this.isCameraOpen) {
                    this.loadCamera()
                }
            },
            loadCamera() {
                this.isCameraOpen = true
                navigator.mediaDevices.getUserMedia(this.videoConstraints).then((stream) => {
                    this.$refs.camera.srcObject = stream
                })
            }
        },

        computed: {
            isModalVisible() {
                return this.isModalOpen;
            }
        },

        mounted(){
            window.addEventListener("load", this.onWindowLoad);
        }

    }
</script>