<script>
	import { init } from 'svelte-i18n';
  // Let's now import some modules
  // and components.

  // Courses List.
  let courses = [
    { 
      id: 0,
      title: "Software Testing and Automation",
      date: new Date()
    },
    {
      id: 1,
      title: "User Experience Design Fundamentals",
      date: new Date()
    },
    {
      id: 2,
      title: "Drawing and Painting with Procreate",
      date: new Date()
    },
    {
      id: 3,
      title: "How To Become A Maste Of Influence",
      date: new Date()
    }
  ];

  // Current page variable.
  // (Contains an index of current
  // page; made for sidebarItems array)
  let currentPage = 1;

  // Sidebar Items array
  let sidebarItems = [
    // Pinned Things
    {
      id: 0,
      icon: "./icons/bookmark.svg",
      title: "Pinned"
    },
    // All Courses
    {
      id: 1,
      icon: "./icons/clipboard.svg",
      title: "All courses"
    },
    // Recourses
    {
      id: 2,
      icon: "./icons/cloud.svg",
      title: "Recourses"
    },
    // Online books
    {
      id: 3,
      icon: "./icons/book.svg",
      title: "Online Books"
    },
    // Settings
    {
      id: 4,
      icon: "./icons/settings.svg",
      title: "Settings"
    }
  ];
</script>

<!-- Main application -->
<main style="min-height: 100vh;" class="w-full flex bg-gray-100 relative">
  <!-- 
    @section Sidebar 
    Just a normal sidebar.
    I dunno what do I need to
    write here, so I'll write
    something.  
  -->
  <div style="height: 100vh; overflow: hidden;" class="relative w-1/6 shadow-sm bg-white">
    
    <!-- Logotype -->
    <div class="text-left py-4 md:py-8 lg:py-12 mx-4 md:mx-8 lg:mx-12 border-solid border-b-2 border-gray-200">
      <h1 class="text-2xl font-semibold">Teachzy</h1>
    </div>

    <!-- 
      Sidebar items
      Fixed height is bad, yeah?
      Yes, but it works! :o -->
    <div style="overflow-y: scroll; height: 40vh;" class="my-6 pr-4 md:pr-6 lg:pr-8">
      {#each sidebarItems as item}
        <div class="py-4 pl-4 md:pl-8 lg:pl-12 flex {currentPage == item.id ? "bg-gray-200 rounded-lg text-indigo-600" : ""}">
          <img style="width: 1.2rem;" src="{item.icon}" alt="Sidebar Icon">
          <p class="mx-4">{item.title}</p>
        </div>
      {/each}
    </div>

    <!-- 
      Logout button
      and promotional
      banner 
    -->
    <div class="absolute inset-x-0 bottom-0 py-6 bg-white">
      <!-- Logout button -->
      <div class="flex pl-4 md:pl-8 lg:pl-12">
        <img style="width: 1.2rem;" src="./icons/log-out.svg" alt="Logout Button">
        <p class="mx-4">Log out</p>
      </div>

      <!-- Promotional banner -->
      <div class="mt-8 flex rounded-lg shadow-xl px-4 py-4 pt-8 mx-8 bg-blue-300">
        <!-- Some text -->
        <div class="text-white text-sm w-full">
          <p>Save big - get mounthly subscription!</p>
        </div>

        <!-- Small button -->
        <div class="w-full flex justify-center items-end">
          <img style="width: 1.2rem;" src="./icons/arrow-right.svg" alt="Arrow Right">
        </div>
      </div>
    </div>
  </div>

  <!-- 
    @section Courses list
    Just another list of current
    courses.
   -->
  <div style="overflow: hidden; height: 100vh;" class="w-2/6">
    <!-- "Header" with search bar and
     notifications icon -->
    <div style="height: 20vh;" class="w-full flex justify-between items-center lg:px-12">
      <!-- Search bar -->
      <div class="px-4 py-3 bg-gray-200 flex text-gray-600 rounded-lg shadow-sm">
        <!-- Icon -->
        <img style="width: 1.2rem;" src="./icons/search.svg" alt="Search Icon">
        <!-- Input -->
        <input class="bg-gray-200 mx-2" type="text" placeholder="Search">
      </div>

      <!-- Notification icon -->
      <div class="p-4 bg-gray-200 shadow-sm rounded-lg">
        <img style="width: 1.2rem;" src="./icons/bell.svg" alt="Notification Icon">
      </div>
    </div>

    <!-- Courses list -->
    <div style="overflow-y: scroll; height: 80vh;" class="w-full h-full lg:pl-16">
      <!-- Course Item -->
      { #each courses as course }
        <div class="flex h-32 my-8">
          <!-- Icon -->
          <div class="w-1/3 relative bg-blue-500 rounded-lg">
            <!-- Date -->
            <div class="absolute left-0 top-0 p-4 text-black">
              <h1 class="text-2xl font-semibold">{course.date.getDay()}</h1>
              <p>Jun</p>
            </div>
          </div>

          <!-- Texts -->
          <div class="w-2/3 items-center mx-6">
            <h1 class="text-black text-xl font-semibold">{course.title}</h1>
          </div>
        </div>
      { /each }
    </div>
  </div>

  <!-- 
    @section Course Information
    Some information about choosed
    Course. 
   -->
  <div style="overflow: scroll; min-height: 100vh;" class="w-3/6 bg-white shadow-sm">
    <!-- "Header" -->
    <div style="height: 20vh;" class="w-full flex justify-between items-center px-6">
      <!-- Links -->
      <div class="flex">
        <p class="mx-4">My courses</p>
        <p class="mx-4">Purchases</p>
        <p class="mx-4">Help</p>
      </div>

      <!-- User Account -->
      <div class="flex items-center">
        <p class="text-gray-700 mx-4">John Alby</p>
        <span style="background: url('https://media.discordapp.net/attachments/661496619249696769/736203739727134790/b1e63fd1-1136-4aec-8b21-3d6e60d6134f.jpg')" class="w-8 h-8 rounded-full"></span>
      </div>
    </div>

    <!-- Course information -->
    <div class="px-6">
      <div class="flex w-full">
        <div class="w-full">
          <!-- Card -->
          <div class="h-40 w-full bg-blue-400 rounded-lg relative">
            <!-- Date -->
            <div class="absolute left-0 top-0 p-4 text-black">
              <h1 class="text-2xl font-semibold">15</h1>
              <p>Jun</p>
            </div>
          </div>

          <!-- Some texts -->
          <div class="mt-6">
            <h1 class="text-xl text-black font-semibold">User Experience Design Fundamentals</h1>
            <p class="mt-4">Gain the basic skills in User Experience. Study practice and theory. Find out techniques and tools used to design efficiently... <span class="text-indigo-700 border-indigo-700 border-solid border-b-2">more...</span></p>

            <!-- Buttons -->
            <div class="mt-6 flex">
              <!-- Buy course -->
              <button class="rounded-lg text-white px-6 py-4 bg-gray-900">
                Buy course
              </button>

              <!-- Reviews -->
              <button class="flex mx-6 items-center">
                <img style="width: 1.2rem;" src="./icons/message-square.svg" alt="Reviews Icon">
                <p class="mx-4">Reviews</p>
              </button>
            </div>
          </div>
        </div>

        <!-- Course Statistics -->
        <div class="w-full h-full flex flex-col justify-center items-center">
          <!-- Start time -->
          <div class="rounded-lg border-dotted border-2 border-indigo-700 py-4 px-12 inline-block text-center">
            <div class="flex justify-center ml-4 items-start">
              <h1 class="text-3xl text-indigo-700 pt-2">02</h1>
              <h2 class="text-sm text-indigo-700 pt-2 border-solid border-b-2 border-indigo-700">30</h2>

              <p class="text-sm text-black mx-2">pm</p>
            </div>

            <p class="text-black mt-2">Starting in</p>
          </div>

          <!-- More -->
          <div class="mt-6">
            <img style="width: 1.8rem;" src="./icons/arrow-down.svg" alt="Show More Info" />
          </div>
        </div>
      </div>
    </div>
  </div>
</main>