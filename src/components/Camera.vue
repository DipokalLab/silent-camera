
<template>
  <header>
    <div class="text-center text-gray-800 h-full">
        <video ref="camera" class="bg-black h-full" :width="1080" :height="1920" autoplay></video>


        <div class="block fixed inset-x-0 bottom-0 z-10 pb-10">
            <button type="button" class="text-white bg-slate-700 hover:bg-slate-800 font-medium rounded-md text-sm px-4 py-4 dark:bg-slate-600 dark:hover:bg-slate-700 focus:outline-none dark:focus:ring-blue-800">
                <span class="material-icons-outlined w-8 h-8 text-2xl">
                photo_camera
                </span>
            </button>
        </div>

    </div>
  </header>
</template>