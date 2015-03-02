# Selecting the ratins type for portlet entities

Since Liferay 7.0 administrators can select portlet entities ratings type using a common interface from Contron Panel.
This selection could be applied at site or portal level.

Developers could contribute with their own implementations defining the ratings type for an entity using OSGI modules. This definition mechanism allows to include more entities to the selection list and  could be applied to both, your own developed portlets but also to Liferay portlets. 

Portal supports out-of-the-box ratings selection for:

* Blogs
* Bookmarks
* Comments
* Document Library
* Message Boards
* Web Content

Due possible data incompatibility we have created a mechanism to allow developers transform the ratings data as
needed. This could be contributed to portal using OSGI OSGI modules that can be deployed individually. Only one 
transform policy could be active and it will be applied to all entities. 

Portal default policy is do not transform data on ratings change, so data is interpreted.

# PortletsDataDefinition

The definitions to ratings type needs to implement `PortletRatingsDefition` interface. The implementation of method `getDefaultRatingsType` will return the ratings type of the entity. The implementation of method `getPortletId` will return the portlet id of the entity. 

Implementations of `PortletRatingsDefition` needs to be registed in OSGI so they can be used by the portal. The way of doing this it's using the OSGI annotation `@Component` with an attribute `model.class.name` with the classname or the classnames affected by this definition.

This is an example of a `PortletRatingsDefition` implementation for the Blogs portlet that will define the ´blogsEntry´ ratings data:

```java
@Component(
	property = {
		"model.class.name=com.liferay.portlet.blogs.model.BlogsEntry"
	}
)
public class BlogsPortletRatingsDefinition implements PortletRatingsDefinition {

	@Override
	public RatingsType getDefaultRatingsType() {
		return RatingsType.THUMBS;
	}

	@Override
	public String getPortletId() {
		return PortletKeys.BLOGS;
	}

}
```

# RatingsDataTransformer

The transformer for ratings data needs to implement `RatingsDataTransformer` interface. The implementation of method `transformRatingsData` will perform the transformation of the data. In order to obtain a fine-grained behaviour framework provides the `fromRatingsType` ant the `toRatingsType`, so developer could transform data as needed, and perform different transformations under different circumbstances.

Implementations of `PortletRatingsDefition` needs to be registed in OSGI so they can be used by the portal. The way of doing this it's using the OSGI annotation `@Component`.

This is an dummie example of a `PortletRatingsDefition` that will reset the score from the ratings type when passing from `LIKE` to `STARS` ratings types. **Developer is responsable of data transformations**. In this case, for example, changes are not restorables:

```java
@Component
public class DummieRatingsDataTransformer implements RatingsDataTransformer {
	@Override
	public ActionableDynamicQuery.PerformActionMethod transformRatingsData(
			final RatingsType fromRatingsType, final RatingsType toRatingsType)
		throws PortalException {

		return new ActionableDynamicQuery.PerformActionMethod() {

			@Override
			public void performAction(Object object)
				throws PortalException {

				if (fromRatingsType.getValue().equals(RatingsType.LIKE) &&
					toRatingsType.getValue().equals(RatingsType.STARS)) {

					RatingsEntry ratingsEntry = (RatingsEntry) object;

					ratingsEntry.setScore(0);

					RatingsEntryLocalServiceUtil.updateRatingsEntry(
						ratingsEntry);
				}
			}
		};
	}

}
```
