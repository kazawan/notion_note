# NOTION api

```jsx
const { Client, isFullPage } = require("@notionhq/client")

const key = 'secret_Yhq35eRCKXnhqMWTLrppYpcXubObxXqwJtPt9bJOUB5'
const dbid = 'f94d692a99e2469a983792aa6b7e15d0'
// https://www.notion.so/f94d692a99e2469a983792aa6b7e15d0

// 初始化客户端
const notion = new Client({
    auth: key,
})

//单个查询
// async function main() {
//     const myPage = await notion.databases.query({
//         database_id: dbid,
//         filter:{
//             property:'Name',
//             rich_text:{
//                 contains:'bob'
//             }
//         }
//     })
//     // let  list = await myPage.results[0].properties
//     console.log(myPage.results[0].properties.Name)
// }

// main()

async function main() {
    // 查询数据库
    const myPage = await notion.databases.query({
        database_id: dbid,
       
    })
    // let  list = await myPage.results[0].properties
    let list = []
    let i = 0 ;
    for(const page of myPage.results){
        if(!isFullPage(page)){
            continue
        }
        // console.log(page.properties.age.multi_select[0].name)
        // 将查询结果添加到列表中
        list.push({
            name:page.properties.Name.title[0].plain_text,
            age:page.properties.age.multi_select[0].name
        })
        
    }
    
    console.log(list)
    
}

main()
```

### 插入数据到 Notion 数据库

如果你想要将数据插入到 Notion 数据库中，你可以使用

@notionhq/client

包提供的

pages.create

方法。以下是一个示例代码：

```jsx
const { Client } = require('@notionhq/client');

// 使用你的 API 密钥初始化一个新的 Notion 客户端
const notion = new Client({ auth: process.env.NOTION_API_KEY });

// 创建一个新页面
const response = await notion.pages.create({
  parent: {
    database_id: process.env.NOTION_DATABASE_ID,
  },
  properties: {
    Name: {
      title: [
        {
          text: {
            content: 'New Page',
          },
        },
      ],
    },
    Description: {
      rich_text: [
        {
          text: {
            content: 'This is a new page created via the Notion API!',
          },
        },
      ],
    },
  },
});

// 打印结果
console.log(response);
```

在这个示例中，我们使用 pages.create 方法创建了一个新页面，并将其插入到 ID 存储在 NOTION_DATABASE_ID 环境变量中的数据库中。我们还指定了页面的名称和描述，这些属性在 Notion 数据库中已经定义。

你可以根据你的需求自定义页面的属性，例如添加多个文本字段、复选框、日期等。请查看 Notion API 文档以获取有关如何使用 API 的更多信息。

希望这可以帮助你开始在 Notion 数据库中插入数据！如果你有任何进一步的问题或需要帮助，请随时让我知道。