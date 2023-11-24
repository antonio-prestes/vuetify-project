<template>
  <div class="min-h-full">
    <div class="bg-indigo-600 pb-32">
      <Disclosure as="nav" class="border-b border-indigo-300 border-opacity-25 bg-indigo-600 lg:border-none"
                  v-slot="{ open }">
        <div class="mx-auto max-w-7xl px-2 sm:px-4 lg:px-8">
          <div
            class="relative flex h-16 items-center justify-between lg:border-b lg:border-indigo-400 lg:border-opacity-25">
            <div class="flex items-center px-2 lg:px-0">
              <div class="flex-shrink-0">
                <img class="block h-8 w-8" src="https://tailwindui.com/img/logos/mark.svg?color=indigo&shade=300"
                     alt="Your Company"/>
              </div>
              <div class="hidden lg:ml-10 lg:block">
                <div class="flex space-x-4">
                  <a v-for="item in navigation" :key="item.name" :href="item.href"
                     :class="[item.current ? 'bg-indigo-700 text-white' : 'text-white hover:bg-indigo-500 hover:bg-opacity-75', 'rounded-md py-2 px-3 text-sm font-medium']"
                     :aria-current="item.current ? 'page' : undefined">{{ item.name }}</a>
                </div>
              </div>
            </div>
            <div class="flex flex-1 justify-center px-2 lg:ml-6 lg:justify-end">
              <div class="w-full max-w-lg lg:max-w-xs">
                <label for="search" class="sr-only">Search</label>
                <div class="relative text-gray-400 focus-within:text-gray-600">
                  <div class="pointer-events-none absolute inset-y-0 left-0 flex items-center pl-3">
                    <MagnifyingGlassIcon class="h-5 w-5" aria-hidden="true"/>
                  </div>
                  <input id="search"
                         class="block w-full rounded-md border-0 bg-white py-1.5 pl-10 pr-3 text-gray-900 focus:ring-2 focus:ring-white focus:ring-offset-2 focus:ring-offset-indigo-600 sm:text-sm sm:leading-6"
                         placeholder="Search" type="search" name="search"/>
                </div>
              </div>
            </div>
            <div class="flex lg:hidden">
              <!-- Mobile menu button -->
              <DisclosureButton
                class="relative inline-flex items-center justify-center rounded-md bg-indigo-600 p-2 text-indigo-200 hover:bg-indigo-500 hover:bg-opacity-75 hover:text-white focus:outline-none focus:ring-2 focus:ring-white focus:ring-offset-2 focus:ring-offset-indigo-600">
                <span class="absolute -inset-0.5"/>
                <span class="sr-only">Open main menu</span>
                <Bars3Icon v-if="!open" class="block h-6 w-6" aria-hidden="true"/>
                <XMarkIcon v-else class="block h-6 w-6" aria-hidden="true"/>
              </DisclosureButton>
            </div>
            <div class="hidden lg:ml-4 lg:block">
              <div class="flex items-center">
                <button type="button"
                        class="relative flex-shrink-0 rounded-full bg-indigo-600 p-1 text-indigo-200 hover:text-white focus:outline-none focus:ring-2 focus:ring-white focus:ring-offset-2 focus:ring-offset-indigo-600">
                  <span class="absolute -inset-1.5"/>
                  <span class="sr-only">View notifications</span>
                  <BellIcon class="h-6 w-6" aria-hidden="true"/>
                </button>

                <!-- Profile dropdown -->
                <Menu as="div" class="relative ml-3 flex-shrink-0">
                  <div>
                    <MenuButton
                      class="relative flex rounded-full bg-indigo-600 text-sm text-white focus:outline-none focus:ring-2 focus:ring-white focus:ring-offset-2 focus:ring-offset-indigo-600">
                      <span class="absolute -inset-1.5"/>
                      <span class="sr-only">Open user menu</span>
                      <img class="h-8 w-8 rounded-full" :src="user.imageUrl" alt=""/>
                    </MenuButton>
                  </div>
                  <transition enter-active-class="transition ease-out duration-100"
                              enter-from-class="transform opacity-0 scale-95"
                              enter-to-class="transform opacity-100 scale-100"
                              leave-active-class="transition ease-in duration-75"
                              leave-from-class="transform opacity-100 scale-100"
                              leave-to-class="transform opacity-0 scale-95">
                    <MenuItems
                      class="absolute right-0 z-10 mt-2 w-48 origin-top-right rounded-md bg-white py-1 shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none">
                      <MenuItem v-for="item in userNavigation" :key="item.name" v-slot="{ active }">
                        <a :href="item.href"
                           :class="[active ? 'bg-gray-100' : '', 'block px-4 py-2 text-sm text-gray-700']">{{
                            item.name
                          }}</a>
                      </MenuItem>
                    </MenuItems>
                  </transition>
                </Menu>
              </div>
            </div>
          </div>
        </div>

        <DisclosurePanel class="lg:hidden">
          <div class="space-y-1 px-2 pb-3 pt-2">
            <DisclosureButton v-for="item in navigation" :key="item.name" as="a" :href="item.href"
                              :class="[item.current ? 'bg-indigo-700 text-white' : 'text-white hover:bg-indigo-500 hover:bg-opacity-75', 'block rounded-md py-2 px-3 text-base font-medium']"
                              :aria-current="item.current ? 'page' : undefined">{{ item.name }}
            </DisclosureButton>
          </div>
          <div class="border-t border-indigo-700 pb-3 pt-4">
            <div class="flex items-center px-5">
              <div class="flex-shrink-0">
                <img class="h-10 w-10 rounded-full" :src="user.imageUrl" alt=""/>
              </div>
              <div class="ml-3">
                <div class="text-base font-medium text-white">{{ user.name }}</div>
                <div class="text-sm font-medium text-indigo-300">{{ user.email }}</div>
              </div>
              <button type="button"
                      class="relative ml-auto flex-shrink-0 rounded-full bg-indigo-600 p-1 text-indigo-200 hover:text-white focus:outline-none focus:ring-2 focus:ring-white focus:ring-offset-2 focus:ring-offset-indigo-600">
                <span class="absolute -inset-1.5"/>
                <span class="sr-only">View notifications</span>
                <BellIcon class="h-6 w-6" aria-hidden="true"/>
              </button>
            </div>
            <div class="mt-3 space-y-1 px-2">
              <DisclosureButton v-for="item in userNavigation" :key="item.name" as="a" :href="item.href"
                                class="block rounded-md px-3 py-2 text-base font-medium text-white hover:bg-indigo-500 hover:bg-opacity-75">
                {{ item.name }}
              </DisclosureButton>
            </div>
          </div>
        </DisclosurePanel>
      </Disclosure>
      <header class="py-10">
        <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
          <h1 class="text-3xl font-bold tracking-tight text-white">Dashboard</h1>
        </div>
      </header>
    </div>

    <main class="-mt-32">
      <div class="mx-auto max-w-7xl px-4 pb-12 sm:px-6 lg:px-8">
        <div class="rounded-lg bg-white px-5 py-6 shadow sm:px-6">
          <div class="px-4 sm:px-6 lg:px-8">
            <div class="sm:flex sm:items-center">
              <div class="sm:flex-auto">
                <DropDownSelect
                  :people="people"
                  @selected-items-changed="handleSelectedItems"
                  @clear-selection="this.filteredPeople = []"
                />
                <h1 class="text-base font-semibold leading-6 text-gray-900">Users</h1>
                <p class="mt-2 text-sm text-gray-700">A list of all the users in your account including their name,
                  title, email and role.</p>
              </div>
              <div class="mt-4 sm:ml-16 sm:mt-0 sm:flex-none">
                <div class="text-center">
                </div>
                <button type="button"
                        class="block rounded-md bg-indigo-600 px-3 py-2 text-center text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">
                  Add user
                </button>
              </div>
            </div>
            <div class="mt-8 flow-root">
              <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
                <div class="inline-block min-w-full py-2 align-middle">
                  <table class="min-w-full divide-y divide-gray-300">
                    <thead>
                    <tr>
                      <th scope="col"
                          class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-6 lg:pl-8">Name
                      </th>
                      <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">Title</th>
                      <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">Email</th>
                      <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">Role</th>
                      <th scope="col" class="relative py-3.5 pl-3 pr-4 sm:pr-6 lg:pr-8">
                        <span class="sr-only">Edit</span>
                      </th>
                    </tr>
                    </thead>
                    <tbody class="divide-y divide-gray-200 bg-white">
                    <tr v-for="person in itemsList" :key="person.email">
                      <td class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-6 lg:pl-8">
                        {{ person.name }}
                      </td>
                      <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ person.title }}</td>
                      <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ person.email }}</td>
                      <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ person.role }}</td>
                      <td
                        class="relative whitespace-nowrap py-4 pl-3 pr-4 text-right text-sm font-medium sm:pr-6 lg:pr-8">
                        <a href="#" class="text-indigo-600 hover:text-indigo-900"
                        >Edit<span class="sr-only">, {{ person.name }}</span></a
                        >
                      </td>
                    </tr>
                    </tbody>
                  </table>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import {Disclosure, DisclosureButton, DisclosurePanel, Menu, MenuButton, MenuItem, MenuItems} from '@headlessui/vue'
import {MagnifyingGlassIcon} from '@heroicons/vue/20/solid'
import {Bars3Icon, BellIcon, XMarkIcon} from '@heroicons/vue/24/outline'
import DropDownSelect from "@/components/DropDownSelect.vue";


export default {
  // eslint-disable-next-line vue/no-reserved-component-names
  components: {
    Disclosure,
    DisclosurePanel,
    DisclosureButton,
    MenuItem,
    MenuItems,
    MenuButton,
    DropDownSelect,
    // eslint-disable-next-line vue/no-reserved-component-names
    Menu,
    MagnifyingGlassIcon,
    Bars3Icon,
    BellIcon,
    XMarkIcon
  },
  data() {
    return {
      user: {
        name: 'Tom Cook',
        email: 'tom@example.com',
        imageUrl:
          'https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
      },
      navigation: [
        {name: 'Dashboard', href: '#', current: true},
        {name: 'Team', href: '#', current: false},
        {name: 'Projects', href: '#', current: false},
        {name: 'Calendar', href: '#', current: false},
        {name: 'Reports', href: '#', current: false},
      ],
      userNavigation: [
        {name: 'Your Profile', href: '#'},
        {name: 'Settings', href: '#'},
        {name: 'Sign out', href: '#'},
      ],
      people: [
        {name: 'Lindsay Walton', title: 'Front-end Developer', email: 'lindsay.walton@example.com', role: 'Member'},
        {name: 'Michael Johnson', title: 'Back-end Developer', email: 'michael.j@example.com', role: 'Member'},
        {name: 'Emily Rodriguez', title: 'UX Designer', email: 'emily.rodriguez@example.com', role: 'Member'},
        {name: 'Daniel Smith', title: 'Full-stack Developer', email: 'daniel.smith@example.com', role: 'Admin'},
        {name: 'Sophie Turner', title: 'Product Manager', email: 'sophie.turner@example.com', role: 'Member'},
        {name: 'Alex Miller', title: 'UI Developer', email: 'alex.m@example.com', role: 'Member'},
        {name: 'Jessica Garcia', title: 'Software Engineer', email: 'jessica.g@example.com', role: 'Member'},
        {name: 'Kevin White', title: 'DevOps Engineer', email: 'kevin.white@example.com', role: 'Admin'},
        {name: 'Megan Brown', title: 'Front-end Designer', email: 'megan.b@example.com', role: 'Member'},
        {name: 'Brian Taylor', title: 'QA Tester', email: 'brian.t@example.com', role: 'Member'},
        {name: 'Olivia Clark', title: 'System Architect', email: 'olivia.clark@example.com', role: 'Admin'},
        {name: 'Christopher Lee', title: 'Mobile App Developer', email: 'chris.lee@example.com', role: 'Member'},
        {name: 'Amanda Wilson', title: 'Database Administrator', email: 'amanda.w@example.com', role: 'Member'},
        {name: 'Samuel Harris', title: 'Network Engineer', email: 'sam.harris@example.com', role: 'Admin'},
        {name: 'Taylor Martinez', title: 'Scrum Master', email: 'taylor.m@example.com', role: 'Member'},
        {name: 'Jordan Hall', title: 'Data Scientist', email: 'jordan.h@example.com', role: 'Member'}
      ],
      selectedItems: [],
      filteredPeople: []
    }
  },
  computed: {
    itemsList() {
      return this.filteredPeople.length > 0 ? this.filteredPeople : this.people;
    }
  },
  methods: {
    handleSelectedItems(selectedItems) {
      this.filteredPeople = selectedItems
    },
    filter() {
      this.filteredPeople = this.people.filter(item =>
        Object.values(item).some(val =>
          val.toString().toLowerCase().includes(this.search.toLowerCase())
        )
      );
    }
  }
}

</script>
