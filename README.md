<p align="center"><img width="100%" src="https://i.imgur.com/2aIi8wF.png"></p>

# Dresser+

An enhanced version of the built-in [Dresser](https://github.com/Facepunch/sbox-public/blob/e94842870561ba24e236c03b214510ba5f649484/engine/Sandbox.Engine/Scene/Components/Game/Dresser.cs) component. Works with both citizens and humans, built-in and custom player controllers.

## 📣 Features

* Body attributes networked and updated in real time across all clients
* Clothing sources are now easier to grasp for beginners
* A new Manual/OwnerUser hybrid clothing source
* Parallel workshop clothing loading

### Clothing Sources

* **Manual** - Dress using hand-picked built-in clothing items or clothing straight from the workshop
* **LocalUser** - Each client sees their own avatar; you can change your avatar in s&box's main menu
* **OwnerUser** - All clients see the network owner's avatar of the GameObject where Dresser+ is attached
* **Hybrid** - Start from the network owner's avatar, strip selected clothing categories, and add hand-picked clothing on top

### Hybrid Source

1. Set `Source` to **Hybrid**
2. Add categories to `StrippedCategories` (e.g. Hat, Jacket, Skin) to remove those slots from the owner's outfit
3. Add your own items to `Clothing` or `WorkshopClothing` to dress your client specific clothes

> *Extremely useful for gamemodes where players keep their identity but wear **role-specific equipment**, like uniforms or team gear.*

### Body Attributes

| Property | Range | Description |
|---|---|---|
| `ManualHeight` | 0.5 - 1.5 | Body height scale |
| `ManualAge` | 0.0 - 1.0 | Skin aging intensity (smooth to wrinkled) - ONLY ON CITIZENS |
| `ManualTint` | 0.0 - 1.0 | Skin color along the tint spectrum - ONLY ON CITIZENS |

> *Editable in **Manual** and **Hybrid** modes. Changes are synced and propagate immediately via `OnManualChange`.*

### Workshop Clothing

* Retrieves clothing from workshop packages using their identifiers
* Fetched and mounted asynchronously at dress time

> *Editable in **Manual** and **Hybrid** modes. A warning will be logged if the package could not be fetched or mounted.*

## 📖 Installation

* Install the DresserPlus library straight from your Library Manager in your s&box editor

 OR

* Download the [DresserPlus.cs](https://github.com/noxtgm/dresser-plus/blob/77bc57a21139906d7f4edab7a7aa4e1a28219da9/Code/DresserPlus.cs) C# script and add it to your project's `Code/` folder

> Once you've done either one of those, add the **Dresser Plus** component to a GameObject with a Citizen or Human body.
> Set the `BodyTarget` to the body's `SkinnedModelRenderer` (auto-detected from children if left empty), pick a clothing source, and you're done.

## 🛜 API

```csharp
// Apply with current settings
await dresser.Apply();

// Apply with new clothing items (e.g. to set different clothes depending on a var in your code)
await dresser.Apply( myClothingList );

// Strip all clothing and reset body attributes
dresser.Clear();

// Cancel an in-progress async dressing operation
dresser.CancelDressing();

// Check if currently dressing
if ( dresser.IsDressing ) { /* ... */ }
```

## ⚙️ Properties

* **BodyTarget** - The `SkinnedModelRenderer` of the body to dress *(auto-detected if empty)*
* **Source** - Which clothing source to use
* **RemoveUnownedItems** - Strip items not in the owner's Steam Inventory *(OwnerUser/Hybrid only)*
* **ApplyHeightScale** - Whether height scaling is active
* **ManualHeight** - Body height scale, 0.5 to 2.0 *(Manual/Hybrid only)*
* **ManualAge** - Skin aging, 0 to 1 *(Manual/Hybrid only)*
* **ManualTint** - Skin color blend, 0 to 1 *(Manual/Hybrid only)*
* **Clothing** - List of clothing entries *(Manual/Hybrid only)*
* **WorkshopClothing** - Workshop package identifiers to fetch *(Manual/Hybrid only)*
* **StrippedCategories** - Clothing categories to remove from the owner's avatar *(Hybrid only)*

## 📄 License

[CC0](https://choosealicense.com/licenses/cc0-1.0/)

<br>

<a href="https://ko-fi.com/noxtgm" target="_blank" rel="noreferrer"><img src="https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExOG00a3RqYTBzcmo2a2UxZGZ6bXl2dDY5Z2w0YmQ0Y2RxMWd0aWM4OSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9cw/bZgsAwXUIVU2tcKn7s/giphy.gif" alt="Support me on Ko-fi" width="240" height="55"/></a>
