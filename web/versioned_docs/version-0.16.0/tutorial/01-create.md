app ETH {
  wasp: {
    version: "^0.16.0"
  },
  title: "ETH",
  client: {
    rootComponent: import { Layout } from "@src/Layout.jsx",
  },
  auth: {
    userEntity: User,
    methods: {
      usernameAndPassword: {}
    },
    onAuthFailedRedirectTo: "/login",
    onAuthSucceededRedirectTo: "/"
  },
}

route LoginRoute { path: "/login", to: LoginPage }
page LoginPage {
  component: import Login from "@src/pages/auth/Login.jsx"
}
route SignupRoute { path: "/signup", to: SignupPage }
page SignupPage {
  component: import Signup from "@src/pages/auth/Signup.jsx"
}

action createCurriculum {
  fn: import { createCurriculum } from "@src/actions.js",
  entities: [Curriculum]
}

action createRecommendation {
  fn: import { createRecommendation } from "@src/actions.js",
  entities: [Curriculum, Recommendation]
}

query getCurriculums {
  fn: import { getCurriculums } from "@src/queries.js",
  entities: [Curriculum]
}

query getRecommendations {
  fn: import { getRecommendations } from "@src/queries.js",
  entities: [Recommendation]
}

route HomeRoute { path: "/", to: HomePage }
page HomePage {
  component: import HomePage from "@src/pages/Home.jsx",
  authRequired: false
}

route CurriculumRoute { path: "/curriculum", to: CurriculumPage }
page CurriculumPage {
  component: import CurriculumPage from "@src/pages/Curriculum.jsx",
  authRequired: true
}

route RecommendationRoute { path: "/recommendation/:curriculumId", to: RecommendationPage }
page RecommendationPage {
  component: import RecommendationPage from "@src/pages/Recommendation.jsx",
  authRequired: true
}
