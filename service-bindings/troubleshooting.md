# Troubleshooting

## Collecting logs from service binding manager

1. Identify the `Pod` that is running the `service-binding-manager` container in the `service-bindings` namespace.

    `$kubectl -n service-bindings get pods`

    For example:
    
    ```bash
    NAME                       READY   STATUS    RESTARTS   AGE
    manager-5dbb5f584c-zvmg2   1/1     Running   0          11d
    ```

2. Gather the actual logs from the `Pod` using the `kubectl` command.
   
   `$ kubectl -n service-bindings logs manager-5dbb5f584c-zvmg2`

   For Example:

   ```bash
    2021/11/05 15:25:28 Registering 3 clients
    2021/11/05 15:25:28 Registering 3 informer factories
    2021/11/05 15:25:28 Registering 7 informers
    2021/11/05 15:25:28 Registering 8 controllers
    {"severity":"INFO","timestamp":"2021-11-05T15:25:28.483823208Z","caller":"logging/config.go:116","message":"Successfully created the logger."}
    {"severity":"INFO","timestamp":"2021-11-05T15:25:28.48392361Z","caller":"logging/config.go:117","message":"Logging level set to: info"}
    {"severity":"INFO","timestamp":"2021-11-05T15:25:28.483999911Z","caller":"logging/config.go:79","message":"Fetch GitHub commit ID from kodata failed","error":"open /var/run/ko/HEAD: no such file or directory"}
    {"severity":"INFO","timestamp":"2021-11-05T15:25:28.484035711Z","logger":"webhook","caller":"profiling/server.go:64","message":"Profiling enabled: false"}
    {"severity":"INFO","timestamp":"2021-11-05T15:25:28.522884909Z","logger":"webhook","caller":"leaderelection/context.go:46","message":"Running with Standard leader election"}
    {"severity":"INFO","timestamp":"2021-11-05T15:25:28.523358615Z","logger":"webhook","caller":"provisionedservice/controller.go:31","message":"Setting up event handlers."}
    ...
    {"severity":"ERROR","timestamp":"2021-11-17T12:30:24.557178813Z","logger":"webhook","caller":"controller/controller.go:548","message":"Reconcile error","duration":"276.504µs","error":"deployments.apps \"spring-petclinic\" not found","stacktrace":"knative.dev/pkg/controller.(*Impl).handleErr\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:548\nknative.dev/pkg/controller.(*Impl).processNextWorkItem\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:531\nknative.dev/pkg/controller.(*Impl).RunContext.func3\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:468"}
    {"severity":"ERROR","timestamp":"2021-11-17T12:47:04.558217679Z","logger":"webhook","caller":"controller/controller.go:548","message":"Reconcile error","duration":"249.103µs","error":"deployments.apps \"spring-petclinic\" not found","stacktrace":"knative.dev/pkg/controller.(*Impl).handleErr\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:548\nknative.dev/pkg/controller.(*Impl).processNextWorkItem\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:531\nknative.dev/pkg/controller.(*Impl).RunContext.func3\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:468"}
    {"severity":"ERROR","timestamp":"2021-11-17T13:03:44.558683121Z","logger":"webhook","caller":"controller/controller.go:548","message":"Reconcile error","duration":"177.403µs","error":"deployments.apps \"spring-petclinic\" not found","stacktrace":"knative.dev/pkg/controller.(*Impl).handleErr\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:548\nknative.dev/pkg/controller.(*Impl).processNextWorkItem\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:531\nknative.dev/pkg/controller.(*Impl).RunContext.func3\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:468"}
    {"severity":"ERROR","timestamp":"2021-11-17T13:20:24.559192644Z","logger":"webhook","caller":"controller/controller.go:548","message":"Reconcile error","duration":"223.203µs","error":"deployments.apps \"spring-petclinic\" not found","stacktrace":"knative.dev/pkg/controller.(*Impl).handleErr\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:548\nknative.dev/pkg/controller.(*Impl).processNextWorkItem\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:531\nknative.dev/pkg/controller.(*Impl).RunContext.func3\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:468"}
    {"severity":"ERROR","timestamp":"2021-11-17T13:37:04.559648412Z","logger":"webhook","caller":"controller/controller.go:548","message":"Reconcile error","duration":"173.003µs","error":"deployments.apps \"spring-petclinic\" not found","stacktrace":"knative.dev/pkg/controller.(*Impl).handleErr\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:548\nknative.dev/pkg/controller.(*Impl).processNextWorkItem\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:531\nknative.dev/pkg/controller.(*Impl).RunContext.func3\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:468"}
    {"severity":"ERROR","timestamp":"2021-11-17T13:53:44.56010516Z","logger":"webhook","caller":"controller/controller.go:548","message":"Reconcile error","duration":"182.402µs","error":"deployments.apps \"spring-petclinic\" not found","stacktrace":"knative.dev/pkg/controller.(*Impl).handleErr\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:548\nknative.dev/pkg/controller.(*Impl).processNextWorkItem\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:531\nknative.dev/pkg/controller.(*Impl).RunContext.func3\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:468"}
    {"severity":"ERROR","timestamp":"2021-11-17T14:10:24.560536033Z","logger":"webhook","caller":"controller/controller.go:548","message":"Reconcile error","duration":"155.603µs","error":"deployments.apps \"spring-petclinic\" not found","stacktrace":"knative.dev/pkg/controller.(*Impl).handleErr\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:548\nknative.dev/pkg/controller.(*Impl).processNextWorkItem\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:531\nknative.dev/pkg/controller.(*Impl).RunContext.func3\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:468"}
    {"severity":"ERROR","timestamp":"2021-11-17T14:27:04.560960243Z","logger":"webhook","caller":"controller/controller.go:548","message":"Reconcile error","duration":"171.002µs","error":"deployments.apps \"spring-petclinic\" not found","stacktrace":"knative.dev/pkg/controller.(*Impl).handleErr\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:548\nknative.dev/pkg/controller.(*Impl).processNextWorkItem\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:531\nknative.dev/pkg/controller.(*Impl).RunContext.func3\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:468"}
    {"severity":"ERROR","timestamp":"2021-11-17T14:43:44.56142548Z","logger":"webhook","caller":"controller/controller.go:548","message":"Reconcile error","duration":"179.203µs","error":"deployments.apps \"spring-petclinic\" not found","stacktrace":"knative.dev/pkg/controller.(*Impl).handleErr\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:548\nknative.dev/pkg/controller.(*Impl).processNextWorkItem\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:531\nknative.dev/pkg/controller.(*Impl).RunContext.func3\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:468"}
    {"severity":"ERROR","timestamp":"2021-11-17T15:00:24.561881861Z","logger":"webhook","caller":"controller/controller.go:548","message":"Reconcile error","duration":"167.902µs","error":"deployments.apps \"spring-petclinic\" not found","stacktrace":"knative.dev/pkg/controller.(*Impl).handleErr\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:548\nknative.dev/pkg/controller.(*Impl).processNextWorkItem\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:531\nknative.dev/pkg/controller.(*Impl).RunContext.func3\n\tknative.dev/pkg@v0.0.0-20210331065221-952fdd90dbb0/controller/controller.go:468"}
   ```