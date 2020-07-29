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
    },

    // Mobile-related
    // links
    {
      id: 5,
      title: "My courses",
      mobile: true
    },
    {
      id: 6,
      title: "Purchases",
      mobile: true
    },    
    {
      id: 7,
      title: "Help",
      mobile: true
    }
  ];

  let menuCollapsed = true;

  let choosedCourse;
  let showStatistics;
</script>

<!-- Main application -->
<main style="min-height: 100vh;" class="w-full flex flex-col md:flex-row bg-gray-100 relative">
  <!-- 
    @section Sidebar 
    Just a normal sidebar.
    I dunno what do I need to
    write here, so I'll write
    something.  
  -->
  <div style="overflow: hidden; z-index: 999;" class="{ menuCollapsed == true ? "md:h-100vh" : "h-full md:h-100vh" } relative md:block w-full md:w-1/6 shadow-sm bg-white">
    
    <!-- Logotype -->
    <div class="w-full flex justify-between items-center">
      <div class="text-left py-4 md:py-8 lg:py-12 mx-4 md:mx-8 lg:mx-12 md:border-solid md:border-b-2 md:border-gray-200">
        <h1 class="text-2xl font-semibold">Teachzy</h1>
      </div>

      <!-- Menu Button (for mobile screns) -->
      <div class="block md:hidden"> 
        {#if menuCollapsed}
          <button on:click={(e) => menuCollapsed = false} class="mx-4 p-4 bg-gray-200 shadow-sm rounded-lg">
            <img style="width: 1.2rem;" src="./icons/menu.svg" alt="Menu Icon">
          </button>
        { :else }
          <button on:click={(e) => menuCollapsed = true} class="mx-4 p-4 bg-gray-200 shadow-sm rounded-lg">
            <img style="width: 1.2rem;" src="./icons/menu.svg" alt="Menu Icon">
          </button>
        {/if}
      </div>
    </div>

    <!-- 
      Sidebar items
      Fixed height is bad, yeah?
      Yes, but it works! :o -->
    <div style="overflow-y: scroll;" class="{menuCollapsed == true ? "hidden md:block md:h-40vh" : "block h-full md:h-40vh"} bg-gray-100 md:bg-white md:my-6 py-8 md:py-0 px-4 md:px-0 md:pr-6">
      {#each sidebarItems as item}
        <div class="py-4 pl-4 md:pl-8 lg:pl-12 {item.mobile == true ? "flex md:hidden" : "flex"} {currentPage == item.id ? "bg-gray-200 rounded-lg text-indigo-600" : ""}">
          {#if item.icon}
            <img style="width: 1.2rem;" src="{item.icon}" alt="Sidebar Icon">
          {/if}
          <p class="mx-4">{item.title}</p>
        </div>
      {/each}

      <!-- User Profile -->
      <div class="flex md:hidden w-full justify-center items-center mt-8">
        <button class="mx-4 rounded-lg text-white px-4 py-2 bg-gray-900">Account</button>
      </div>
    </div>

    <!-- 
      Logout button
      and promotional
      banner 
    -->
    <div class="hidden md:block absolute inset-x-0 bottom-0 py-6 bg-white">
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
  <div class="w-full md:w-5/6 h-full flex">
    <div style="overflow: hidden; height: 100vh;" class="w-full md:w-5/12 { choosedCourse != null ? "hidden md:block" : "" } px-4 md:px-0">
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
      <div style="overflow-y: scroll;" class="h-full md:h-80vh w-full h-full lg:pl-16">
        <!-- Course Item -->
        { #each courses as course }
          <div style="cursor: pointer;" on:click={(e) => { choosedCourse = true; }} class="relative flex h-32 my-8">
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
    <div style="overflow: scroll; min-height: 100vh;" class="w-full { choosedCourse == null ? "hidden md:block" : "" } md:w-7/12 bg-white shadow-sm">
      <!-- "Header" -->
      <div style="height: 20vh;" class="w-full hidden md:flex justify-between items-center px-6">
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
        <!-- Choose another course button -->
        <div class="lg:hidden w-full my-8">
          <button on:click={(e) => choosedCourse = null} class="flex">
            <img style="width: 1.2rem;" src="./icons/chevron-left.svg" alt="Chevron Left">
            <p class="mx-4">Course List</p>
          </button>
        </div>

        {#if choosedCourse}
          <div class="flex flex-col md:flex-row w-full">
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
                <div class="mt-6 w-full md:w-auto flex justify-between md:justify-none">
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

            <!-- Show statistics button -->
            {#if !showStatistics}
              <div class="md:hidden w-full flex justify-center items-center py-4 mt-12 text-gray-800">
                <img style="width: 1.2rem;" class="mr-4" src="./icons/arrow-down.svg" alt="Arrow Down">
                <button on:click={(e) => showStatistics = true }>Show More statistics</button>
              </div>
            { :else }
              <div class="md:hidden w-full flex justify-center items-center py-4 mt-12">
                <img style="width: 1.2rem;" class="mr-4" src="./icons/arrow-up.svg" alt="Arrow Up">
                <button on:click={(e) => showStatistics = false}>Show Less statistics</button>
              </div>
            {/if}

            <div class="w-full h-full { showStatistics ? "flex" : "hidden md:flex" } flex-col justify-center items-center mt-12 lg:mt-0">
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
        {/if}
      </div>
    </div>
  </div>
</main>