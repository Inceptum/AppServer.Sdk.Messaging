# AppServer.Sdk.Messaging
Assembly exposes public extension method `ConfigureFromBundle` for `MessagingFacility` class. This method is used to load messaging transport configurations from app server configuration bundle, usually called `transports`.

```
using Inceptum.AppServer.Configuration;
using Inceptum.AppServer.Sdk.Messaging;
using Inceptum.Messaging.Castle;
using Inceptum.Messaging.Contract;
using Inceptum.Messaging.RabbitMq;

public class Installer : IWindsorInstaller
{
  public void Install(IWindsorContainer container, IConfigurationStore store)
  {
    container.AddFacility<MessagingFacility>(f => f
                .ConfigureFromBundle("transports", "{environment}", "{machineName}")
                .WithTransportFactory<RabbitMqTransportFactory>()
                .VerifyEndpoints(EndpointUsage.Subscribe | EndpointUsage.Publish, true, "requests")
                .VerifyEndpoints(EndpointUsage.Publish, true, "responses")
                );
  }
}
```
