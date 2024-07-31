<template>
  <div class="min-h-screen bg-blue-400">
    <Toast />
    <ConfirmDialog />
    <NuxtLayout>
      <div class="flex-1 flex  justify-content-between border-round border-2 p-4 bg-blue-300 border-blue-400 ">
        <NuxtLink to="/" class="no-underline text-0">Home</NuxtLink>
        <NuxtLink to="/notifiche" class="no-underline text-0">Notifiche</NuxtLink>
        <NuxtLink to="/carrellospesa" class="no-underline text-0">Carrello spesa</NuxtLink>
        <NuxtLink to="/fetchricerca" class="no-underline text-0">Fetch con id</NuxtLink>
        <NuxtLink to="/fetch" class="no-underline text-0">Fetch statica</NuxtLink>
        <NuxtLink to="/crud" class="no-underline text-0">Crud</NuxtLink>
        <NuxtLink to="/fakeregister" class="no-underline text-0">Fake Register</NuxtLink>
        <NuxtLink to="/filter" class="no-underline text-0">Filter</NuxtLink>
        <NuxtLink to="/listacard" class="no-underline text-0">Lista Card</NuxtLink>
        <NuxtLink to="/modal" class="no-underline text-0">Modale</NuxtLink>
        <NuxtLink to="/quiz" class="no-underline text-0">quiz</NuxtLink>
        <NuxtLink to="/starrating" class="no-underline text-0">Star rating</NuxtLink>
        <NuxtLink to="/todo" class="no-underline text-0">Todo</NuxtLink>
        <NuxtLink to="/toolbar" class="no-underline text-0">Toolbar</NuxtLink>
      </div>
      <NuxtPage/>
    </NuxtLayout>
  </div>
</template>

<style>
body {
  margin: 0;
  padding: 0;
}
</style>
