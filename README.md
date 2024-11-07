# WinForms publish size

https://github.com/dotnet/winforms/issues/9911

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

## 5. Manually delete WPF dll files: 22M

D3DCompiler_47_cor3.dll, PenImc_cor3.dll, PresentationNative_cor3.dll, vcruntime140_cor3.dll, wpfgfx_cor3.dll

## Last: ReadyToRun

File size not changed much.
