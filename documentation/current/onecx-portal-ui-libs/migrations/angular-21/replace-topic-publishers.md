# Replace removed topic publisher classes

In OneCX libs v8, deprecated publisher wrapper classes were removed from `@onecx/integration-interface` topic APIs.

If your app still uses these classes, TypeScript compilation will fail.

## [](#%5Fremoved%5Fclasses)Removed classes

* `CurrentLocationPublisher`
* `EventsPublisher`
* `ParametersPublisher`
* `ResizedEventsPublisher`

## [](#%5Frequired%5Fmigration)Required migration

Replace publisher wrappers with their corresponding topic classes.

| Removed in v8            | Use instead          |
| ------------------------ | -------------------- |
| CurrentLocationPublisher | CurrentLocationTopic |
| EventsPublisher          | EventsTopic          |
| ParametersPublisher      | ParametersTopic      |
| ResizedEventsPublisher   | ResizedEventsTopic   |

### [](#%5Fexample)Example

Before

```typescript
import { EventsPublisher } from '@onecx/integration-interface'

const eventsPublisher$ = new EventsPublisher()
eventsPublisher$.publish({ type: 'authentication#logoutButtonClicked' })
```

After

```typescript
import { EventsTopic } from '@onecx/integration-interface'

const eventsTopic = new EventsTopic()
eventsTopic.publish({ type: 'authentication#logoutButtonClicked' })
```
