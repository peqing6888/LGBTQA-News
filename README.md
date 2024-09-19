# LGBTQA-News
LGBTQA+ News
1. 需求分析
· 用户注册和登录
· 发布新闻链接和讨论主题
· 评论功能
· 投票系统
· 新闻排序（热门 最新等）
· 用户个人页面
· 搜索功能

2. 数据库设计
· Users 表:
 · id, username, email, password_hash, karma, created_at
· Posts 表:
 · id, title, url, text, user_id, score, comment_count, created_at
· Comments 表:
 · id, text, user_id, post_id, parent_comment_id, created_at
· Votes 表:
 · id, user_id, post_id, comment_id, vote_type

3. API设计 (GraphQL):
    type Query {
     posts(sort: String, limit: Int): [Post]
     post(id: ID!): Post
     user(id: ID!): User
     comments(postId: ID!): [Comment]
     search(query: String!): [Post]
   }

   type Mutation {
     createUser(input: CreateUserInput!): User
     createPost(input: CreatePostInput!): Post
     createComment(input: CreateCommentInput!): Comment
     vote(postId: ID, commentId: ID, voteType: VoteType!): VoteResult
   }

   type Post {
     id: ID!
     title: String!
     url: String
     text: String
     user: User!
     score: Int!
     commentCount: Int!
     createdAt: DateTime!
     comments: [Comment]
   }

   type User {
     id: ID!
     username: String!
     karma: Int!
     createdAt: DateTime!
     posts: [Post]
     comments: [Comment]
   }

   type Comment {
     id: ID!
     text: String!
     user: User!
     post: Post!
     parentComment: Comment
     createdAt: DateTime!
   }
