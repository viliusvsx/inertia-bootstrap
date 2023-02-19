<script setup>
import {Link} from '@inertiajs/vue3';
</script>

<template>
   <div>
       <nav class="navbar navbar-expand-md navbar-light bg-white shadow-sm">
           <div class="container">
               <a class="navbar-brand" href="/">
                   Laravel
               </a>
               <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                   <span class="navbar-toggler-icon"></span>
               </button>

               <div class="collapse navbar-collapse" id="navbarSupportedContent">

                   <!-- Right Side Of Navbar -->
                   <ul class="navbar-nav ms-auto">
                       <!-- Authentication Links -->
                      <div v-if="$page.props.auth.user">
                          <li class="nav-item dropdown">
                              <a id="navbarDropdown" class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                                  {{ $page.props.auth.user.name }}
                              </a>
                              <div class="dropdown-menu dropdown-menu-end" aria-labelledby="navbarDropdown">
                                  <Link class="dropdown-item" :href="route('profile.edit')">
                                      Profile
                                  </Link>
                                  <Link class="dropdown-item" :href="route('logout')" method="post">
                                      Logout
                                  </Link>
                              </div>
                          </li>
                      </div>
                       <div v-else class="d-flex flex-row gap-2">
                           <li class="nav-item">
                               <Link class="btn btn-primary" :href="route('login')">Login</Link>
                           </li>
                           <li class="nav-item">
                               <Link class="btn btn-secondary" :href="route('register')">Register</Link>
                           </li>
                       </div>
                   </ul>
               </div>
           </div>
       </nav>

       <header class="bg-white" v-if="$slots.header">
           <div class="card-header">
               <slot name="header" />
           </div>
       </header>

       <main class="py-3">
           <slot />
       </main>
   </div>
</template>


