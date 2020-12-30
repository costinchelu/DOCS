Working with Arrays in MongoDB
==============================
1. Introduction
--------------------------------------------------------------------------------------------------------------------

In a MongoDB database, data is stored in **collections** and a
collection has **documents**. A document has **fields** and values, like
in a JSON. The field types include **scalar types** (`string`, `number`,
`date`, etc.) and **composite types** (`arrays` and `objects`). In this
article we will look at an example of using the array field type.

The example is an application where users create blog posts and write
comments for the posts. The relationship between the posts and comments
is One-to-Many; i.e., a post can have many comments. We will consider a
collection of blog posts with their comments. That is a post document
will also store the related comments. In MongoDB's document model, a 1:N
relationship data can be stored within a collection; this is a
de-normalized form of data. The related data is stored together and can
be accessed (and updated) together. The comments are stored as an array;
an array of comment objects.

A sample document of the blog posts with comments:

    {
            "_id" : ObjectId("5ec55af811ac5e2e2aafb2b9"),
            "name" : "Working with Arrays",
            "user" : "Database Rebel",
            "desc" : "Maintaining an array of objects in a document",
            "content" : "some content ...",
            "created" : ISODate("2020-05-20T16:28:55.468Z"),
            "updated" : ISODate("2020-05-20T16:28:55.468Z"),
            "tags" : [ "mongodb", "arrays" ],
            "comments" : [
                    {
                            "user" : "DB Learner",
                            "content" : "Nice post.",
                            "updated" : ISODate("2020-05-20T16:35:57.461Z")
                    }
            ]
    }

In an application, a blog post is created, comments are added, queried,
modified or deleted by users. In the example, we will write code to
create a blog post document, and do some CRUD operations with comments
for the post.

2. Create and Query a Document 
--------------------------------------------------------------------------------------------------------------------------------------------------

Let's create a blog post document. We will use a database called as
`blogs` and a collection called as `posts`. The code is written in
`mongo`shell (an interactive JavaScript interface to MongoDB). Mongo
shell is started from the command line and is connected to the MongoDB
server. From the shell:

    use blogs

    NEW_POST =
      { 
        name: "Working with Arrays",
        user: "Database Rebel",
        desc: "Maintaining an array of objects in a document",
        content: "some content...",
        created: ISODate(),
        updated: ISODate(),
        tags: [ "mongodb", "arrays" ]
    }

    db.posts.insertOne(NEW_POST)

Returns a result
`{ "acknowledged" : true, "insertedId" : ObjectId("5ec55af811ac5e2e2aafb2b9") }`
indicating that a new document is created. This is a common
acknowledgement when you perform a write operation. When a document is
inserted into a collection for the first time, the collection gets
created (if it doesn't exist already). The `insertOne` method inserts a
document into the collection.

Now, let's **query** the collection :

    db.posts.findOne()
    {
            "_id" : ObjectId("5ec55af811ac5e2e2aafb2b9"),
            "name" : "Working with Arrays",
            "user" : "Database Rebel",
            "desc" : "Maintaining an array of objects in a document",
            "content" : "some content...",
            "created" : ISODate("2020-05-20T16:28:55.468Z"),
            "updated" : ISODate("2020-05-20T16:28:55.468Z"),
            "tags" : [
                    "mongodb",
                    "arrays"
            ]
    }

The `findOne` method retrieves one matching document from the
collection. Note the scalar fields `name` (string type) and `created`
(date type), and the array field `tags`. In the newly inserted document
there are no comments, yet.

3. Add an Array Element
------------------------------------------------------------------------------------------------------------------------------------

Let's add a comment for this post, by a user "DB Learner":

    NEW_COMMENT = {
      user: "DB Learner",
      text: "Nice post, can I know more about the arrays in MongoDB?",
      updated: ISODate()
    }

    db.posts.updateOne( 
      { _id : ObjectId("5ec55af811ac5e2e2aafb2b9") },
      { $push: { comments: NEW_COMMENT } }
    )

Returns:  
`{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }`

The `updateOne` method updates a document's fields based upon the
specified *condition*. `$push` is an **array update operator** which
adds an element to an array. If the array doesn't exist, it creates an
array field and then adds the element.

Let's query the collection and confirm the new comment visually, using
the `findOne` method:

    {
            "_id" : ObjectId("5ec55af811ac5e2e2aafb2b9"),
            "name" : "Working with Arrays",
            ...
            "comments" : [
                    {
                            "user" : "DB Learner",
                            "text" : "Nice post, can I know more about the arrays in MongoDB?",
                            "updated" : ISODate("2020-05-20T16:35:57.461Z")
                    }
            ]
    }

Note the `comments` array field has comment objects as elements. Let's
add one more comment using the same `$push` update operator. This new
comment (by `user` "Database Rebel") is appended to the `comments`
array:

    "comments" : [
            {
                "user" : "DB Learner",
                "text" : "Nice post, can I know more about the arrays in MongoDB?",
                "updated" : ISODate("2020-05-20T16:35:57.461Z")
            },
            {
                "user" : "Database Rebel",
                "text" : "Thank you, please look for updates",
                "updated" : ISODate("2020-05-20T16:48:25.506Z")
            }
    ]

4. Update an Array Element
------------------------------------------------------------------------------------------------------------------------------------------

Let's update the comment posted by "Database Rebel" with modified `text`
field :

`NEW_CONTENT = "Thank you, please look for updates - updated the post"`.

    db.posts.updateOne( 
      { _id : ObjectId("5ec55af811ac5e2e2aafb2b9"), "comments.user": "Database Rebel" },
      { $set: { "comments.$.text": NEW_CONTENT } }
    )

The `$set` **update operator** is used to change a field's value. The
**positional \$ operator** identifies an element in an array to update
without explicitly specifying the position of the element in the array.
The first matching element is updated. The updated comment object:

    "comments" : [
                    {
                            "user" : "Database Rebel",
                            "text" : "Thank you, please look for updates - updated",
                            "updated" : ISODate("2020-05-20T16:48:25.506Z")
                    }
     ]

5. Delete an Array Element
------------------------------------------------------------------------------------------------------------------------------------------

The user changed his mind and wanted to delete the comment, and then add
a new one.

    db.posts.updateOne( 
      { _id" : ObjectId("5ec55af811ac5e2e2aafb2b9") },
      { $pull: { comments: { user: "Database Rebel" } } }
    )

The `$pull` **update operator** removes elements from an array which
match the specified *condition* - in this case
`{ comments: { user: "Database Rebel" } }`.

A new comment is added to the array after the above delete operation,
with the following text:
`"Thank you for your comment. I have updated the post with CRUD operations on an array field"`.

6. Add a New Field to all Objects in the Array
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Let's add a new field `likes` for all the comments in the array.

    db.posts.updateOne( 
      { "_id : ObjectId("5ec55af811ac5e2e2aafb2b9") },
      { $set: { "comments.$[].likes": 0 } }
    )

The **all positional operator** `$[]` specifies that the update operator
`$set` should modify all elements in the specified array field. After
the update, all comment objects have the `likes` field, for example:

    {
        "user" : "DB Learner",
        "text" : "Nice post, can I know more about the arrays in MongoDB?",
        "updated" : ISODate("2020-05-20T16:35:57.461Z"),
        "likes" : 0
    }

7. Update a Specific Array Element Based on a Condition
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

First, let's add another new comment using the `$push` update operator:

    NEW_COMMENT = {
      user: "DB Learner",
      text: "Thanks for the updates!",
      updated: ISODate()
    }

Note the `likes` field is missing in the input document. We will update
this particular comment in the `comments` array with the *condition*
that the `likes` field is missing.

    db.posts.updateOne( 
      { "_id" : ObjectId("5ec55af811ac5e2e2aafb2b9") },
      { $inc: { "comments.$[ele].likes": 1 } },
      { arrayFilters: [ { "ele.user": "DB Learner",  "ele.likes": { $exists: false } } ] }
    )

The `likes` field is updated using the `$inc` **update operator** (this
increments a field's value, or if not exists adds the field and then
increments). The **filtered positional operator** `$[<identifier>]`
identifies the array elements that match the `arrayFilters` conditions
for an update operation.

* * * * *

8. Conclusion
----------------------------------------------------------------------------------------------------------------

This article showed doing basic CRUD operations on an array of objects:

-   Creating and adding elements to an array.
-   Querying, updating and deleting an array element.
-   Updating all array elements or a specific element based upon a
    condition.

MongoDB also allows **indexing the array elements** - in this case,
fields of the comment objects of the `comments` array. For example, if
you are querying on the comments by `"comments.user"` and need fast
access, you can create an index for that field. Indexes on array fields
are called as **Multikey Indexes**. Array field indexes can be part of
**Compound Indexes**.

We can do many other **operations on the arrays** - *projections*,
*querying* and *updating* - using various operators as well as the
**Aggregation Pipeline**. Also, perform these operations on **nested
arrays** (arrays within arrays). We will see some of these features in a
later article.

* * * * *
[**](https://www.codementor.io/@prasadsaya/working-with-arrays-in-mongodb-16s303gkd3#81-useful-links)