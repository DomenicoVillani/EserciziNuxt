
<script setup>
import { ref } from 'vue';

const products = ref([
    {
        id: 1,
        name: 'Product 1',
        image: 'https://media.istockphoto.com/id/1367357589/it/foto/cielo-rosso-a-forma-di-cuore-al-tramonto-bellissimo-paesaggio-con-fiori-adoro-lo-sfondo-con-lo.jpg?s=612x612&w=0&k=20&c=6Kg0qxN65TrVE2jenTslGJmn_rnrx9d1d1A1UV91K58=', // Assicurati che queste immagini esistano nella cartella /static/images del tuo progetto Nuxt
        price: 100,
        inventoryStatus: 'INSTOCK'
    },
    {
        id: 2,
        name: 'Product 2',
        image: 'https://thumbs.dreamstime.com/b/superficie-praticante-il-surfing-dell-acqua-onda-di-oceano-mare-124362369.jpg',
        price: 200,
        inventoryStatus: 'LOWSTOCK'
    },
    {
        id: 3,
        name: 'Product 3',
        image: 'https://i.pinimg.com/736x/ba/a6/39/baa639bc2e4405c6e01665bc33dae70a.jpg',
        price: 300,
        inventoryStatus: 'LOWSTOCK'
    },
    {
        id: 3,
        name: 'Product 3',
        image: 'https://markcom.it/wp-content/uploads/2015/12/immagini-per-siti-web.jpg',
        price: 300,
        inventoryStatus: 'INSTOCK'
    },{
        id: 3,
        name: 'Product 3',
        image: 'https://i0.wp.com/www.giacomocusano.com/wp-content/uploads/2016/07/coastal-wash-web.jpg?resize=1024%2C675&ssl=1',
        price: 300,
        inventoryStatus: 'OUTOFSTOCK'
    }
    ,{
        id: 3,
        name: 'Product 3',
        image: 'https://www.chimerarevo.com/wp-content/uploads/2020/04/immagini-gratis.jpg',
        price: 300,
        inventoryStatus: 'INSTOCK'
    }
    ,
    {
        id: 3,
        name: 'Product 3',
        image: 'https://media.istockphoto.com/id/1317323736/it/foto/una-vista-nel-cielo-direzione-alberi.jpg?s=612x612&w=0&k=20&c=Yztgdkk4Ghoqtdgp3SgR_MxNodkbOqs3A8LYF3wnsos=',
        price: 300,
        inventoryStatus: 'LOWSTOCK'
    },{
        id: 3,
        name: 'Product 3',
        image: 'https://static.vecteezy.com/ti/foto-gratuito/p1/2030159-tramonto-sulla-spiaggia-tropicale-gratuito-foto.jpg',
        price: 300,
        inventoryStatus: 'INSTOCK'
    }
    ,{
        id: 3,
        name: 'Product 3',
        image: 'https://www.fotografareperstupire.com/wp-content/uploads/2020/03/immagini-ad-alta-risoluzione-gratis.jpg',
        price: 300,
        inventoryStatus: 'INSTOCK'
    }
]);

const responsiveOptions = ref([
    {
        breakpoint: '1400px',
        numVisible: 2,
        numScroll: 1
    },
    {
        breakpoint: '1199px',
        numVisible: 3,
        numScroll: 1
    },
    {
        breakpoint: '767px',
        numVisible: 2,
        numScroll: 1
    },
    {
        breakpoint: '575px',
        numVisible: 1,
        numScroll: 1
    }
]);

const getSeverity = (status) => {
    switch (status) {
        case 'INSTOCK':
            return 'success';
        case 'LOWSTOCK':
            return 'warning';
        case 'OUTOFSTOCK':
            return 'danger';
        default:
            return null;
    }
};
</script>


<template>
    <div class="flex justify-content-center m-6 text-0 text-2xl">
        <h1>HOME PAGE</h1>
    </div>
    <div class="card m-5">
        <Accordion :activeIndex="0">
            <AccordionTab header="Header I">
                <p class="m-0">
                    Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
                    consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
                </p>
            </AccordionTab>
            <AccordionTab header="Header II">
                <p class="m-0">
                    Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim
                    ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Consectetur, adipisci velit, sed quia non numquam eius modi.
                </p>
            </AccordionTab>
            <AccordionTab header="Header III">
                <p class="m-0">
                    At vero eos et accusamus et iusto odio dignissimos ducimus qui blanditiis praesentium voluptatum deleniti atque corrupti quos dolores et quas molestias excepturi sint occaecati cupiditate non provident, similique sunt in culpa qui
                    officia deserunt mollitia animi, id est laborum et dolorum fuga. Et harum quidem rerum facilis est et expedita distinctio. Nam libero tempore, cum soluta nobis est eligendi optio cumque nihil impedit quo minus.
                </p>
            </AccordionTab>
        </Accordion>
    </div>
    <div class="card py-5 mt-5">
        <Carousel :value="products" :numVisible="3" :numScroll="3" :responsiveOptions="responsiveOptions">
            <template #item="slotProps">
                <div class="border-1 surface-border border-round m-2 p-3 surface-100">
                    <div class="mb-3">
                        <div class="relative mx-auto">
                            <img :src="slotProps.data.image" :alt="slotProps.data.name" class="w-full border-round" />
                            <Tag :value="slotProps.data.inventoryStatus" :severity="getSeverity(slotProps.data.inventoryStatus)" class="absolute" style="left:5px; top: 5px"/>
                        </div>
                    </div>
                    <div class="mb-3 font-medium">{{ slotProps.data.name }}</div>
                    <div class="flex justify-content-between align-items-center">
                        <div class="mt-0 font-semibold text-xl">${{ slotProps.data.price }}</div>
                        <span>
                            <Button icon="pi pi-heart" severity="secondary" />
                            <Button icon="pi pi-shopping-cart" class="ml-2"/>
                        </span>
                    </div>
                </div>
            </template>
        </Carousel>
    </div>
</template>