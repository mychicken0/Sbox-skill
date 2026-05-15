# Resources And Prefabs

Use resources for designer-authored data and prefabs for reusable object graphs.

## GameResource Definition

```csharp
[AssetType( Name = "Item Definition", Extension = "itemdef", Category = "Game",
	Flags = AssetTypeFlags.NoEmbedding | AssetTypeFlags.IncludeThumbnails )]
public sealed class ItemDefinition : GameResource
{
	[Property, Group( "Display" )] public string Title { get; set; } = "Unnamed";
	[Property, Group( "Display" )] public Texture Icon { get; set; }
	[Property, Group( "Spawn" )] public PrefabFile Prefab { get; set; }
	[Property, Group( "Balance" ), Range( 1, 999 )] public int Price { get; set; } = 10;

	public static IReadOnlyList<ItemDefinition> All()
		=> ResourceLibrary.GetAll<ItemDefinition>().OrderBy( x => x.Title ).ToArray();

	public static ItemDefinition Get( string path )
		=> string.IsNullOrWhiteSpace( path ) ? null : ResourceLibrary.Get<ItemDefinition>( path );
}
```

## Resource Rules

- Put data that designers tune in `GameResource`.
- Keep runtime state out of resources.
- Give asset extensions short clear names.
- Use `CreateAssetTypeIcon` or `RenderThumbnail` only when it improves editor browsing.
- If publishing matters, implement `ConfigurePublishing` to reject invalid assets.

## Prefab Rules

- Prefer prefab references over hardcoded model/material/component setup.
- Spawn prefabs on the host for networked gameplay objects.
- Set parent and `GameObjectFlags.NotNetworked` for local-only helper objects such as post-process rigs.
- Use `StartEnabled = false` when you need to configure components before enabling.

## Lookup Patterns

```csharp
var def = ResourceLibrary.Get<MyDefinition>( resourcePath );
var all = ResourceLibrary.GetAll<MyDefinition>();
var byPrefab = all.FirstOrDefault( x => x.Prefab?.ResourcePath == prefabPath );
```

## Avoid

- Do not scan resources every frame.
- Do not mutate shared resource assets as gameplay state.
- Do not duplicate resource catalogs if `ResourceLibrary.GetAll<T>()` is sufficient.
