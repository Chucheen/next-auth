<script setup lang="ts">
import { useSession, signIn, signOut, computed } from '#imports'

const { data: session, status } = useSession()
const loading = computed(() => status.value === 'loading')
</script>

<template>
  <header>
    <div class="signedInStatus">
      <p :class="['nojs-show', !session && loading ? 'loading' : 'loaded']">
        <template v-if="session">
          <span v-if="session.user?.image" :style="{ backgroundImage: `url(${session.user.image})` }" class="avatar" />
          <span class="signedInText">
            <small>Signed in as</small><br>
            <strong>{{ session.user?.email || session.user?.name }}</strong>
          </span>
          <a href="/api/auth/signout" class="button" @click.prevent="signOut">Sign out</a>
        </template>
        <template v-else>
          <span class="notSignedInText">You are not signed in</span>
          <a href="/api/auth/signin" class="buttonPrimary" @click.prevent="signIn">Sign in</a>
        </template>
      </p>
    </div>
    <nav>
      <ul class="navItems">
        <li class="navItem">
          <NuxtLink to="/">
            Home
          </NuxtLink>
        </li>
        <li class="navItem">
          <NuxtLink to="/client">
            Client
          </NuxtLink>
        </li>
        <li class="navItem">
          <NuxtLink to="/server">
            Server
          </NuxtLink>
        </li>
        <li class="navItem">
          <NuxtLink to="/protected">
            Protected
          </NuxtLink>
        </li>
        <li class="navItem">
          <NuxtLink to="/api-example">
            API
          </NuxtLink>
        </li>
      </ul>
    </nav>
  </header>
</template>

<style>
.nojs-show {
  opacity: 1;
  top: 0;
}

.signedInStatus {
display: block;
min-height: 4rem;
width: 100%;
}

.loading,
.loaded {
position: relative;
top: 0;
opacity: 1;
overflow: hidden;
border-radius: 0 0 .6rem .6rem;
padding: .6rem 1rem;
margin: 0;
background-color: rgba(0,0,0,.05);
transition: all 0.2s ease-in;
}

.loading {
top: -2rem;
opacity: 0;
}

.signedInText,
.notSignedInText {
position: absolute;
padding-top: .8rem;
left: 1rem;
right: 6.5rem;
white-space: nowrap;
text-overflow: ellipsis;
overflow: hidden;
display: inherit;
z-index: 1;
line-height: 1.3rem;
}

.signedInText {
padding-top: 0rem;
left: 4.6rem;
}

.avatar {
border-radius: 2rem;
float: left;
height: 2.8rem;
width: 2.8rem;
background-color: white;
background-size: cover;
background-repeat: no-repeat;
}

.button,
.buttonPrimary {
float: right;
margin-right: -.4rem;
font-weight: 500;
border-radius: .3rem;
cursor: pointer;
font-size: 1rem;
line-height: 1.4rem;
padding: .7rem .8rem;
position: relative;
z-index: 10;
background-color: transparent;
color: #555;
}

.buttonPrimary {
background-color: #346df1;
border-color: #346df1;
color: #fff;
text-decoration: none;
padding: .7rem 1.4rem;
}

.buttonPrimary:hover {
box-shadow: inset 0 0 5rem rgba(0,0,0,0.2)
}

.navItems {
margin-bottom: 2rem;
padding: 0;
list-style: none;
}

.navItem {
display: inline-block;
margin-right: 1rem;
}
</style>
