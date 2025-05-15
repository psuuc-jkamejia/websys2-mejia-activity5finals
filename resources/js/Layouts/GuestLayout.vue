<template>
  <div class="min-h-screen flex flex-col items-center pt-6 sm:pt-0">
    <!-- Your custom logo -->
        <div class="flex items-center">
            <Link :href="route('dashboard')">
                <img src="/images/new-logo.png" alt="Logo" class="h-10" />
            </Link>
        </div>
    <div class="w-full sm:max-w-md px-6 py-4 bg-white/90 shadow-md rounded">
      <slot />
    </div>
  </div>
</template>

