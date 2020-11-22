Function ShowGPOStatus
{
    [CmdletBinding()]
    Param
    (
        [parameter(Mandatory=$true)][String]$GPOStatus
    )

    Write-Verbose "Checking the Status of Group Policies depanding on the first parameter value as AllSettingsDisabled or AllSettingsEnabled"
    
    (Get-ADForest).domains | 
        Foreach-Object { 
            Get-GPO -All -Domain $_ | Where-Object { $_.GPOStatus -eq $GPOStatus } 
        } |
        Select-Object -Property DisplayName | Sort-Object DisplayName
}

$disabledCount = (ShowGPOStatus -GPOStatus "AllSettingsDisabled").Count
$enabledCount = (ShowGPOStatus -GPOStatus "AllSettingsEnabled").Count

<#
 # Exsamples:
 Get-Help ShowGPOStatus
 ShowGPOStatus -GPOStatus "AllSettingsDisabled" -Verbose
 ShowGPOStatus -GPOStatus "AllSettingsEnabled" -Verbose
 ShowGPOStatus -GPOStatus "AllSettingsDisabled"
 (ShowGPOStatus -GPOStatus "AllSettingsDisabled").Count
 ShowGPOStatus -GPOStatus "AllSettingsEnabled"
 (ShowGPOStatus -GPOStatus "AllSettingsEnabled").Count
 Write-Host "At the domain $((Get-ADForest).domains) are $disabledCount disabled GPOs." -ForegroundColor Red | ShowGPOStatus -GPOStatus "AllSettingsDisabled"
 Write-Host "At the domain $((Get-ADForest).domains) are $enabledCount enabled GPOs." -ForegroundColor Green | ShowGPOStatus -GPOStatus "AllSettingsEnabled"
 Clear
#>
