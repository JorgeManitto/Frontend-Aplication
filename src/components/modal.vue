<template>
    <section @click="close()"  class="h-screen w-screen bg-gray-500 fixed top-0 opacity-50 z-10" >
        </section>
         <div class="absolute inset-0">
            <div class="flex h-full ">
                <div class="mx-56 fixed z-20 bg-white p-2 rounded shadow  w-2/3">
                    <div class="py-2 border">
                        <h2 class="text-2xl">
                             <slot name="title"></slot>
                        </h2>
                        <h4>
                            <slot name="year"></slot>
                        </h4>
                         <div >
                             <slot name="img"></slot>
                        </div>
                        <div class="font-mono">
                             <slot name="body"></slot>
                        </div>
                        
                    </div>
                </div>
            </div>
        </div>
</template>
<script>
export default {
     emits: ["close"],
    setup(_,{emit}) {
        function close() {
            emit("close");
        }

        return {close}
    }
}
</script>