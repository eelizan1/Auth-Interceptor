# Angular Authentication

Simple authentication application with login and register page using JWT.

JWTs are used in authentication to securely transfer information between two parties, typically the user and the server. When we login we get a token after that which need to pass that token in the header for any other remaining calls.

## Main Features

Interceptor
Routing
JWT's

## Testing

To test we will use a free api with the curl

```
curl -X 'POST' \
  'https://freeapi.miniprojectideas.com/api/User/Login' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json-patch+json' \
  -d '{
  "EmailId": "chetan@gmail.com",
  "Password": "admin"
}'
```

## Routing

```
const routes: Routes = [
  {
    path: 'login',
    component: LoginComponent,
  },
  {
    path: '',
    redirectTo: 'login',
    pathMatch: 'full',
  },
  {
    // once user logins, all the components should be rendered here
    path: '',
    component: LayoutComponent,
    children: [
      {
        path: 'dashboard',
        component: DashboardComponent,
      },
    ],
  },
  {
    // wildcard path
    path: '**',
    component: LoginComponent,
  },
];

```

## Interceptor

Allows us to send the JWT token along with any other API calls after a succesful login

```
@Injectable()
export class CustomInterceptor implements HttpInterceptor {

  constructor() {}

  intercept(request: HttpRequest<unknown>, next: HttpHandler): Observable<HttpEvent<unknown>> {
    return next.handle(request);
  }
}
```

In app module

```
providers: [
    {
      provide: HTTP_INTERCEPTORS,
      useClass: CustomInterceptor,
      multi: true,
    },
]
```
