<template>
  <table class="table">
    <thead class="thead-dark">
      <tr>
        <th scope="col">#</th>
        <th scope="col">Category</th>
        <th scope="col">Name</th>
        <th scope="col" width="300">操作</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="restaurant in restaurants" :key="restaurant.id">
        <th scope="row">
          {{ restaurant.id }}
        </th>
        <td>{{ restaurant.Category ? restaurant.Category.name : "未分類" }}</td>
        <td>{{ restaurant.name }}</td>
        <td class="d-flex justify-content-between">
          <router-link
            :to="{ name: 'admin-restaurant', params: { id: restaurant.id } }"
            class="btn btn-link"
            >Show</router-link
          >

          <router-link
            :to="{
              name: 'admin-restaurant-edit',
              params: { id: restaurant.id },
            }"
            class="btn btn-link"
            >Edit</router-link
          >

          <button
            type="button"
            class="btn btn-link"
            @click="deleteRestaurant(restaurant.id)"
          >
            Delete
          </button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
const dummyData = {
  restaurants: [
    {
      id: 7,
      name: "Priscilla Weimann",
      tel: "413-275-8040 x8807",
      address: "13397 Boyd Springs",
      opening_hours: "08:00",
      description:
        "Et adipisci culpa. Repellat et qui alias ut iste eum. Non veritatis tempora eos blanditiis molestiae. Unde modi ut fugit.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=93.76182351773355",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 1,
      Category: {
        id: 1,
        name: "中式料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 10,
      name: "Alisha Terry III",
      tel: "(015) 052-0301",
      address: "33064 Labadie Square",
      opening_hours: "08:00",
      description: "cum",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=75.86577157393457",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 1,
      Category: {
        id: 1,
        name: "中式料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 16,
      name: "Martina Bechtelar",
      tel: "488.563.9255 x94176",
      address: "1018 Angelina Corners",
      opening_hours: "08:00",
      description: "Maiores ad enim quisquam esse.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=73.00166527529986",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 1,
      Category: {
        id: 1,
        name: "中式料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 23,
      name: "Dianna Osinski V",
      tel: "730.701.3131 x85683",
      address: "54975 Bode Motorway",
      opening_hours: "08:00",
      description:
        "Aperiam aspernatur ut iusto placeat laborum et id repudiandae.\nEst quae et id.\nPerferendis eum enim eligendi eos quidem dolorem.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=21.6994683198134",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 1,
      Category: {
        id: 1,
        name: "中式料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 27,
      name: "Neal Mills",
      tel: "1-378-412-1624 x93771",
      address: "0803 Cruickshank Point",
      opening_hours: "08:00",
      description: "dolores qui et",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=8.294942495766211",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 1,
      Category: {
        id: 1,
        name: "中式料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 33,
      name: "Wilhelm Graham II",
      tel: "302.709.3497",
      address: "542 Anita Gardens",
      opening_hours: "08:00",
      description:
        "Omnis at et quisquam ut illo voluptatem incidunt. Quia modi consequatur omnis et consectetur voluptas earum. Sit et dolores dicta recusandae molestiae et molestiae et.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=44.278523875162534",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 1,
      Category: {
        id: 1,
        name: "中式料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 37,
      name: "Sydni O'Kon",
      tel: "1-449-070-9922 x79069",
      address: "8725 Marvin Glens",
      opening_hours: "08:00",
      description:
        "Voluptas corporis quasi quis sapiente dolorem velit qui. Sit ratione et officiis et doloremque eius enim soluta. Architecto voluptate quisquam harum rerum soluta ea ea. Temporibus quod laboriosam omnis dolorem voluptatibus ea.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=79.05416765036021",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 1,
      Category: {
        id: 1,
        name: "中式料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 40,
      name: "Brenden Russel PhD",
      tel: "759-867-4838",
      address: "3525 Olson Junction",
      opening_hours: "08:00",
      description:
        "Dolores totam sit et consectetur. Qui quia dignissimos ratione doloremque ut amet saepe eos. Voluptatibus perspiciatis quo. Sunt itaque ut velit dolor repudiandae quia dolorum rerum. Aliquid ea exercitationem rem neque sed eius commodi.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=58.132611981809454",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 1,
      Category: {
        id: 1,
        name: "中式料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 3,
      name: "Erika Kohler",
      tel: "688.166.1376",
      address: "6274 Leonora Glens",
      opening_hours: "08:00",
      description:
        "Nisi voluptatem odit quam atque esse qui. Et et quasi magni vel. Dolore est modi architecto eligendi sed voluptatem natus. Necessitatibus commodi aperiam nisi minus amet eum nostrum.\n \rExercitationem non officia alias ut nihil. Voluptas ut sit facere sunt quidem minima nihil iure. Natus amet labore quis rerum aut molestiae.\n \rNon animi itaque officia corrupti eos veniam. Facilis quia fugiat ut debitis nemo eveniet ab voluptatem. Quis quas repellat tempore autem. Quibusdam quos assumenda. Eum possimus consequuntur suscipit. Placeat autem ut itaque aperiam distinctio.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=89.09004118949329",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 2,
      Category: {
        id: 2,
        name: "日本料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 4,
      name: "Dr. Joanne Schiller",
      tel: "139.032.1777",
      address: "59479 Balistreri Drive",
      opening_hours: "08:00",
      description: "veritatis",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=25.116136783468445",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 2,
      Category: {
        id: 2,
        name: "日本料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 29,
      name: "Roma Romaguera",
      tel: "702.960.3496",
      address: "016 Fredrick Hill",
      opening_hours: "08:00",
      description: "voluptatem",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=31.569986212483904",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 2,
      Category: {
        id: 2,
        name: "日本料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 38,
      name: "Jonathan Larkin",
      tel: "(895) 107-9200 x84692",
      address: "80844 Amalia Walk",
      opening_hours: "08:00",
      description:
        "Adipisci nihil atque rerum pariatur facere sed alias. Neque ea omnis enim dolore autem nulla officiis. Voluptatem suscipit libero impedit velit magni maxime beatae. Cum illo nisi enim saepe qui. Fuga nisi sed quia voluptatem quo inventore provident. Qui ut expedita aut expedita aliquam natus et aut.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=51.47531079696761",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 2,
      Category: {
        id: 2,
        name: "日本料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 41,
      name: "Sigrid Strosin",
      tel: "1-418-777-8368 x7390",
      address: "261 Deion Radial",
      opening_hours: "08:00",
      description:
        "Et quia asperiores neque rerum eius blanditiis ea quia. Fugiat reiciendis quos. Est sit sunt delectus animi voluptatem ipsam eligendi quam. Dolores ipsa dolorum error magnam autem ea eligendi esse.\n \rImpedit consequatur sed qui corrupti nulla accusamus voluptatem quaerat. Distinctio est similique. Ut iusto quis sed voluptatem. Tempore quas ipsa et autem ipsa.\n \rOfficia sit porro aspernatur eos. Quisquam cumque et. Quam veritatis sed doloribus id ut sapiente eos. Omnis id ipsam odio placeat sit consequatur. Praesentium voluptas voluptatum eum est. Accusamus id nobis voluptas et ratione placeat eum.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=66.04245648248374",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 2,
      Category: {
        id: 2,
        name: "日本料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 42,
      name: "Henderson Heidenreich",
      tel: "(959) 244-9756",
      address: "07916 Yoshiko Well",
      opening_hours: "08:00",
      description:
        "Eveniet dolorem omnis nesciunt occaecati vero.\nEst qui ut.\nDolor atque quia qui ipsa delectus sit.\nInventore perspiciatis et ullam qui.\nMolestiae qui quae quidem aut.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=86.00069104840597",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 2,
      Category: {
        id: 2,
        name: "日本料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 43,
      name: "Pete Thiel",
      tel: "(889) 847-6490 x3958",
      address: "2996 Verdie Mission",
      opening_hours: "08:00",
      description:
        "Deleniti magni quos ut culpa. Rerum assumenda neque maxime molestiae impedit facilis repellat. Quia eligendi quia temporibus ut. Id maiores aut voluptas adipisci veritatis. Aut voluptatem pariatur eius et aspernatur voluptatibus reiciendis accusamus.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=71.30821048417295",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 2,
      Category: {
        id: 2,
        name: "日本料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 2,
      name: "Shyanne Schamberger",
      tel: "(415) 455-8000 x0053",
      address: "45155 Leonie Forge",
      opening_hours: "08:00",
      description: "reiciendis est officia",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=26.95346949336752",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 3,
      Category: {
        id: 3,
        name: "義大利料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 8,
      name: "Otilia Funk",
      tel: "1-824-643-8935 x81767",
      address: "294 Schiller Key",
      opening_hours: "08:00",
      description:
        "Laboriosam voluptatum rerum illo ut ullam ut repellendus id. Aperiam quidem sequi aliquid eum aut aut. Ipsam non non. Rerum voluptatem autem saepe.\n \rDignissimos neque nesciunt nulla sed. Ducimus sed et. Voluptate voluptatibus illo adipisci.\n \rEt officia qui fuga aspernatur molestiae dolor quae aut distinctio. Reiciendis qui impedit atque repudiandae praesentium quis dolor et eos. Cum quia quia laboriosam voluptatem quas accusamus. Mollitia voluptatibus voluptas qui distinctio sed et. Harum consequatur accusamus corrupti corrupti. Dicta amet et vitae.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=9.915371048241429",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 3,
      Category: {
        id: 3,
        name: "義大利料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 14,
      name: "Willa Bednar Sr.",
      tel: "965.771.7473 x4070",
      address: "79717 Jerome Rest",
      opening_hours: "08:00",
      description: "Quidem laborum aliquid quasi blanditiis fuga.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=24.31252514186728",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 3,
      Category: {
        id: 3,
        name: "義大利料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 18,
      name: "Krystal Krajcik",
      tel: "288-047-3971",
      address: "3348 Fannie Route",
      opening_hours: "08:00",
      description:
        "Eum debitis a culpa nihil nisi praesentium non eum dolore. Sequi doloribus natus. Sed aperiam dolores porro ea. Qui assumenda doloribus ad omnis ut pariatur ducimus vitae ducimus. Repellendus tempora dicta dolorum sit aut perspiciatis in.\n \rArchitecto omnis adipisci beatae vitae rerum aut eum aspernatur. Perferendis minima est atque consectetur cupiditate harum. Non asperiores ratione. Vitae aut dolor. Explicabo beatae voluptatem voluptas provident voluptate. Reprehenderit facere harum dignissimos.\n \rCorrupti dicta ut sed. Ea quo officiis harum harum aut. Quos id qui. Aliquid ratione voluptatibus odio. Ducimus et aliquam natus illo. Nulla aperiam corporis voluptas dolorem consequatur.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=23.03103233104715",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 3,
      Category: {
        id: 3,
        name: "義大利料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 19,
      name: "Mr. Cicero Yundt",
      tel: "(691) 532-8008 x3470",
      address: "29663 Ernest Prairie",
      opening_hours: "08:00",
      description:
        "Tempore accusamus excepturi laudantium eligendi qui maxime.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=12.204731769207356",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 3,
      Category: {
        id: 3,
        name: "義大利料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 25,
      name: "Eden Heller",
      tel: "(291) 972-5214 x06680",
      address: "32989 Hirthe Gateway",
      opening_hours: "08:00",
      description:
        "Est molestiae reprehenderit alias laudantium quia non libero quas nemo.\nEt aspernatur est et maiores.\nNemo voluptate error minima rerum aut harum omnis qui nostrum.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=19.618933650219226",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 3,
      Category: {
        id: 3,
        name: "義大利料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 32,
      name: "Danny Labadie",
      tel: "(156) 023-6111 x6734",
      address: "983 Meggie Glens",
      opening_hours: "08:00",
      description:
        "Et nam suscipit nemo voluptatem vel. Maiores voluptatem voluptas assumenda. Minus consequatur laudantium officiis sapiente eos cumque vel. Fugit tempore at natus asperiores voluptatem. Porro est at eligendi voluptates assumenda.\n \rQuidem totam enim perferendis. Veritatis velit ex corporis ut tempore. Dolores aut molestiae nobis quibusdam commodi sunt neque. Aliquid qui voluptas corrupti necessitatibus at aperiam eos. Sit quia aut et necessitatibus explicabo.\n \rSed hic dolores et nam quia vel necessitatibus. Accusantium aliquam commodi. Consequatur necessitatibus facere et pariatur dolore non. Veritatis est eos qui sint quos et. Non molestias similique corporis voluptatem asperiores et.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=29.040329150617694",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 3,
      Category: {
        id: 3,
        name: "義大利料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 44,
      name: "Lydia Jakubowski",
      tel: "(732) 091-2375 x229",
      address: "583 Renner Landing",
      opening_hours: "08:00",
      description:
        "Necessitatibus quia ea. Maiores aut reiciendis id et fugit hic exercitationem deleniti vero. Corporis sunt commodi. Distinctio aut veritatis non voluptate eum quia aliquam doloremque nam.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=33.808049400375054",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 3,
      Category: {
        id: 3,
        name: "義大利料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 46,
      name: "Stuart West",
      tel: "388.301.6131",
      address: "3662 Hammes Mills",
      opening_hours: "08:00",
      description: "Recusandae culpa amet.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=5.74606446224708",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 3,
      Category: {
        id: 3,
        name: "義大利料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 47,
      name: "Justen Vandervort",
      tel: "076.968.5062 x39648",
      address: "606 Domenico Villages",
      opening_hours: "08:00",
      description: "quos qui voluptatem",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=50.84909258609835",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 3,
      Category: {
        id: 3,
        name: "義大利料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 48,
      name: "Dr. Broderick Nienow",
      tel: "905-703-3937 x638",
      address: "616 Kaycee Dam",
      opening_hours: "08:00",
      description: "Modi qui omnis illo.\nArchitecto omnis quas consequatur.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=31.289979343651233",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 3,
      Category: {
        id: 3,
        name: "義大利料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 1,
      name: "Dr. Ignacio Schaden",
      tel: "1-117-260-8931",
      address: "4699 Sanford Parkway",
      opening_hours: "08:00",
      description:
        "Odio dolores id tempore.\nIncidunt aut saepe voluptates in voluptatem non labore saepe.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=64.80864812274613",
      viewCounts: 1,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-11T13:03:33.000Z",
      CategoryId: 4,
      Category: {
        id: 4,
        name: "墨西哥料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 6,
      name: "Royce Cummerata",
      tel: "113.997.3143",
      address: "626 Timmothy Roads",
      opening_hours: "08:00",
      description: "voluptatem rerum sint",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=38.4752127607771",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 4,
      Category: {
        id: 4,
        name: "墨西哥料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 9,
      name: "Dr. Marina Hilll",
      tel: "(583) 898-7076",
      address: "853 O'Keefe Course",
      opening_hours: "08:00",
      description:
        "Et rerum omnis animi velit enim.\nAt pariatur mollitia quibusdam explicabo voluptas doloremque nostrum.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=14.825573329294905",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 4,
      Category: {
        id: 4,
        name: "墨西哥料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 11,
      name: "Vern Auer",
      tel: "(987) 576-5219",
      address: "66534 Aisha Vista",
      opening_hours: "08:00",
      description: "Officia enim consequatur et perspiciatis ipsa et odio.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=88.60565947867667",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 4,
      Category: {
        id: 4,
        name: "墨西哥料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 13,
      name: "Yazmin Marquardt",
      tel: "1-780-421-9912 x26442",
      address: "84071 Fred Canyon",
      opening_hours: "08:00",
      description:
        "Est quaerat nulla. Mollitia quas voluptatem. Exercitationem occaecati ex aut expedita.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=8.249294716275358",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 4,
      Category: {
        id: 4,
        name: "墨西哥料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 17,
      name: "Ms. Angel Schroeder",
      tel: "479.173.4020",
      address: "6982 Stanton Bypass",
      opening_hours: "08:00",
      description:
        "Aut dolorem itaque dignissimos assumenda magni quo velit necessitatibus voluptatem. Repellendus autem voluptas rem quisquam. Reprehenderit enim ea accusamus. Quisquam vero esse expedita vel iusto quam illo consequuntur maiores. Blanditiis vel debitis recusandae. Voluptatem error sed.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=52.42233000355392",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 4,
      Category: {
        id: 4,
        name: "墨西哥料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 22,
      name: "Gillian Dickens",
      tel: "(041) 106-5319",
      address: "2480 Beer Pines",
      opening_hours: "08:00",
      description: "Doloremque sunt illum quia.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=78.47472623752823",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 4,
      Category: {
        id: 4,
        name: "墨西哥料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 26,
      name: "Fatima Pfeffer",
      tel: "475-714-7869",
      address: "779 Luigi Pines",
      opening_hours: "08:00",
      description: "Nulla qui quasi ipsa quos quibusdam.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=79.21493593012418",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 4,
      Category: {
        id: 4,
        name: "墨西哥料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 30,
      name: "Cyrus O'Keefe",
      tel: "852.790.3124 x9485",
      address: "820 Holden Heights",
      opening_hours: "08:00",
      description:
        "Consequuntur delectus dolor ex earum qui eius enim. Officia ea itaque quae ratione. Perspiciatis ut itaque sit accusantium ex consequatur. Nemo eos quasi numquam quas consequuntur. Autem suscipit aut temporibus laudantium nobis itaque consequatur. Dolor perspiciatis harum rerum nesciunt cupiditate.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=26.964421319947384",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 4,
      Category: {
        id: 4,
        name: "墨西哥料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 34,
      name: "Kenny Braun",
      tel: "268-494-5993 x94523",
      address: "31882 Jadon Village",
      opening_hours: "08:00",
      description: "omnis",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=84.33192771329638",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 4,
      Category: {
        id: 4,
        name: "墨西哥料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 49,
      name: "Ova Beer",
      tel: "1-146-778-5744 x50348",
      address: "06146 Fay Mills",
      opening_hours: "08:00",
      description: "et id modi",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=18.952178128506624",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 4,
      Category: {
        id: 4,
        name: "墨西哥料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 5,
      name: "Icie Little",
      tel: "1-008-084-8081 x679",
      address: "889 Blanda Unions",
      opening_hours: "08:00",
      description:
        "At quia dicta vel magnam et ut perspiciatis officiis dolorem. Possimus rerum expedita sapiente ut omnis dolorum vel placeat.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=87.74422300180635",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 5,
      Category: {
        id: 5,
        name: "素食料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 12,
      name: "Hardy Upton",
      tel: "(295) 158-2368 x9192",
      address: "296 Gislason Way",
      opening_hours: "08:00",
      description:
        "Eius aliquid molestiae laborum maiores et et similique error et. Ea nihil necessitatibus aliquam sunt mollitia provident minima eligendi. Debitis libero sed. Qui officiis eligendi qui sunt ducimus eveniet quos voluptatem. Id porro voluptatem vel saepe enim est quia. Fuga consectetur dolorem nemo nobis odio eum aut.\n \rExplicabo facilis fuga dicta molestias ut ab iusto. Voluptatem quasi dolor sit consequatur facere non impedit. Minima assumenda ut sit. Dolores perspiciatis ut.\n \rEx quam inventore officiis voluptatem facilis. Placeat ipsa at consequatur et placeat provident rem. Eos quia ab.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=92.52648308484585",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 5,
      Category: {
        id: 5,
        name: "素食料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 15,
      name: "Lydia Will",
      tel: "1-844-913-2726",
      address: "23055 Streich Mews",
      opening_hours: "08:00",
      description:
        "Aut nulla ipsa quia sunt atque ut rerum delectus voluptates.\nEx modi quas perferendis autem.\nA provident quae sit ea quos id autem.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=78.98779585558219",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 5,
      Category: {
        id: 5,
        name: "素食料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 20,
      name: "Uriel Russel",
      tel: "264.406.0828 x1385",
      address: "3319 Gusikowski Knolls",
      opening_hours: "08:00",
      description:
        "In nobis ipsum. Et sed sint. Quasi maxime qui quibusdam corporis adipisci ratione quos quia. Id laboriosam sit molestiae ex qui ipsam. Sit veniam et accusantium voluptas eveniet odit. Tenetur perferendis officia illum commodi.\n \rEa consequatur enim dolores. Vero porro similique. Distinctio nihil libero recusandae.\n \rEt saepe qui harum. Omnis ad consequatur voluptatibus et temporibus. Quos rerum animi aut. Illo ab nostrum. Corrupti atque deserunt. Optio laborum eius illo rerum iste saepe consequuntur ut.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=44.25965396857738",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 5,
      Category: {
        id: 5,
        name: "素食料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 21,
      name: "Ellen Mraz",
      tel: "146-872-4399 x8994",
      address: "759 Israel Bridge",
      opening_hours: "08:00",
      description: "maiores vero deserunt",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=28.283026883839966",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 5,
      Category: {
        id: 5,
        name: "素食料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 24,
      name: "Jess Kautzer",
      tel: "827-836-2135",
      address: "8540 Huels Bridge",
      opening_hours: "08:00",
      description: "Et qui est officiis alias qui ut facere.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=16.16602312774782",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 5,
      Category: {
        id: 5,
        name: "素食料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 28,
      name: "Euna Rowe",
      tel: "1-716-708-5642",
      address: "27069 Champlin Summit",
      opening_hours: "08:00",
      description: "harum",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=94.66661135472425",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 5,
      Category: {
        id: 5,
        name: "素食料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 31,
      name: "Thurman McDermott",
      tel: "1-708-615-5541",
      address: "99837 Aileen Viaduct",
      opening_hours: "08:00",
      description: "est",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=49.20890322232798",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 5,
      Category: {
        id: 5,
        name: "素食料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 35,
      name: "Ms. Imelda Greenholt",
      tel: "1-745-351-5517",
      address: "9684 Markus Isle",
      opening_hours: "08:00",
      description:
        "Deserunt eligendi soluta atque rerum cumque quia dolore aliquid. Ea et ut sed sit rerum quis vel. Molestias fuga omnis accusantium a eaque ut nemo voluptas. Voluptatum exercitationem at sint est unde quas nesciunt.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=76.28831481180005",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 5,
      Category: {
        id: 5,
        name: "素食料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 36,
      name: "Herminia Rippin",
      tel: "(549) 219-7879 x372",
      address: "963 Strosin Throughway",
      opening_hours: "08:00",
      description:
        "Ut aspernatur neque velit quidem nobis eius. Doloremque soluta qui et eligendi dolor consequatur dolores eum dolorum. Autem at excepturi fuga. Est id commodi excepturi sit nisi corrupti et nobis tempora. Quas neque qui reiciendis libero corporis porro. Enim dignissimos molestiae nulla eveniet dolorem.\n \rFuga sed sunt explicabo doloribus. Officia sed et nisi. Accusantium iure assumenda repellendus maxime. Repellendus ea omnis maxime dignissimos quas omnis aut libero. Enim tenetur ad qui consequuntur. Et pariatur consectetur quasi.\n \rBlanditiis et delectus autem. Omnis aperiam in et quibusdam aut quos autem sed. Explicabo quasi sequi dignissimos qui dolorem odit dolorem omnis.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=37.527396543510584",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 5,
      Category: {
        id: 5,
        name: "素食料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 39,
      name: "Lonie Aufderhar",
      tel: "989-463-4211",
      address: "0604 Kassulke Station",
      opening_hours: "08:00",
      description: "Corporis ullam unde quaerat doloremque nihil explicabo.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=20.415705962394103",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 5,
      Category: {
        id: 5,
        name: "素食料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 45,
      name: "Jakob Pacocha I",
      tel: "371-768-7764",
      address: "9059 Herzog Prairie",
      opening_hours: "08:00",
      description: "ullam",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=92.0026309496549",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 5,
      Category: {
        id: 5,
        name: "素食料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
    {
      id: 50,
      name: "Micah Satterfield",
      tel: "682-342-8160 x9691",
      address: "7227 Vito Brooks",
      opening_hours: "08:00",
      description:
        "Voluptatem numquam quaerat enim enim assumenda reprehenderit necessitatibus rerum. Autem et laboriosam rerum atque eius. Enim sit distinctio amet. Placeat autem non quas neque quis quos. Optio incidunt impedit.\n \rSaepe sint accusantium porro quis vero saepe aut enim. Voluptates molestiae consequatur dolorem blanditiis blanditiis fuga et sunt eligendi. Possimus amet quo cum voluptatem et consequatur vel possimus. Consequatur et dolorem.\n \rIpsa corrupti possimus fugit recusandae iste necessitatibus vel voluptate. Ullam fugiat adipisci assumenda. Ut ipsam sint cumque voluptatem. Veritatis provident voluptatem suscipit molestiae illo ullam.",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=34.26518521942723",
      viewCounts: 0,
      createdAt: "2021-11-07T16:49:43.000Z",
      updatedAt: "2021-11-07T16:49:43.000Z",
      CategoryId: 5,
      Category: {
        id: 5,
        name: "素食料理",
        createdAt: "2021-11-07T16:49:43.000Z",
        updatedAt: "2021-11-07T16:49:43.000Z",
      },
    },
  ],
};

export default {
  data() {
    return {
      restaurants: [],
    };
  },
  created() {
    this.fetchRestaurants();
  },
  methods: {
    fetchRestaurants() {
      this.restaurants = dummyData.restaurants;
    },
    deleteRestaurant(restaurantId) {
      this.restaurants = this.restaurants.filter(
        (restaurant) => restaurant.id !== restaurantId
      );
    },
  },
};
</script>