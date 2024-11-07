# WinForms publish size



## 1. default: 160M
default settings.

## 2. PublishAot: 62M

```xml
	<PublishAot>true</PublishAot>
	<_SuppressWinFormsTrimError>true</_SuppressWinFormsTrimError>
```
Manually delete .pdb file

## 3. RemoveWPFReference: 33M

add to .csproj
```csproj
  <Target Name="RemoveWPFReference" BeforeTargets="WriteIlcRspFileForCompilation">
  	<ItemGroup>
  		<IlcReference Remove="@(IlcReference)" Condition="'%(Filename)' == 'PresentationFramework'" />
  	</ItemGroup>
  </Target>
```  

## 4. Remove network: 30M
in .csproj
```csproj
  <PropertyGroup>
  	<XmlResolverIsNetworkingEnabledByDefault>false</XmlResolverIsNetworkingEnabledByDefault>
  </PropertyGroup>
  <ItemGroup>
  	<!-- We really should introduce a first class property for this -->
  	<RuntimeHostConfigurationOption Include="System.Windows.Forms.PictureBox.UseWebRequest" Value="false" Trim="true" />
  </ItemGroup>
```