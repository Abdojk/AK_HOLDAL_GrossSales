# AK_HOLDAL_GrossSales

D365 F&O extension model that adds a **Gross Sales** display column to the Sales Order Lines inquiry form.

## Business Requirement

- **Formula**: Gross Sales = SalesPrice x SalesQty
- **Scope**: All line statuses (Open, Invoiced, Cancelled)
- **Behaviour**: Display method (read-only, no storage, no filtering)
- **Export**: Included in Export to Excel via `[SysClientCacheDataMethod(true)]`

## Model Structure

```
HoldalGrossSales/
  HoldalGrossSales/
    Descriptor/
      HoldalGrossSales.xml              Model descriptor (v1.0.0.0)
    AxClass/
      SalesLine_HoldalExtension.xml     Table extension class with grossSales display method
    AxFormExtension/
      SalesLine.HoldalGrossSales.xml    Form extension adding Gross Sales column to grid
```

## AOT Objects

| Object | Type | Purpose |
|--------|------|---------|
| `SalesLine_HoldalExtension` | Class (ExtensionOf SalesLine) | Defines `grossSales` static display method |
| `SalesLine.HoldalGrossSales` | Form Extension | Adds Gross Sales control to the SalesLine grid |

## Dependencies

- ApplicationPlatform
- ApplicationFoundation
- ApplicationSuite

## Deployment Notes

### Pre-deployment verification required

1. **Form AOT name**: The form extension assumes `SalesLine` is the AOT form name for "Sales and Marketing > Inquiries and Reports > Sales Order Lines". Verify in the target environment: right-click the form title bar > Form Information > confirm AOT name.
2. **Grid control name**: The extension assumes `LineViewGrid` as the grid control name. Inspect the base form in Visual Studio to confirm.
3. **SalesPrice field**: Confirm `SalesLine.SalesPrice` is the correct unit price field (not a derived/overridden price).
4. **EDT**: Using `SalesAmount` as the return type. Verify compilation succeeds.

## Client

Holdal (requested by Zeina Keyrouz, MIS Manager)
