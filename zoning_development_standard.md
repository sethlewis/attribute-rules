
// Calculation Attribute Rule Using Reference Table
// trigers: Insert, Update
// field: ZoningCode

// get the first related row from Table LANDUSE.DevelopmentStandard
var key = $feature.ZoningCode
var reference_info = FeatureSetByName($datastore, "LANDUSE.DevelopmentStandard", ["*"], false)
var reference_info = First(Filter(reference_info, "zoning_code = @Key"))

// abort if no related row was found
if(reference_info == null) { 

return {"errorMessage": 'There is no corresponding key in the reference table.'}

}

else {
// return the related row's attributes
return {
    "result": {
        'attributes': {
            'HeightMax': Number(reference_info.height_maximum, '###'),
            'CoverageMinimum': reference_info.coverage_maximum,
            'LandscapeMinimum': reference_info.landscape_minimum,
            'SiteMinimum': reference_info.site_area_minimum,
            'LotDepth': reference_info.lot_depth_minimum,
            'LotWidth': reference_info.lot_width_minimum,
            'SetbackFront': reference_info.front_setback_minimum,
            'SetbackRear': reference_info.rear_setback_minimum,
            'SetbackSide': reference_info.side_setback_minimum,
            'SetbackStreet': reference_info.street_side_setback_minimum,
            'DensityMaximum': reference_info.density_maximum,
            'PFSMinimum': reference_info.parking_front_setback_minimum,
            'OSFSMinimum': reference_info.open_front_setback_minimum,
            'CWSSMinimum': reference_info.common_rear_setback_minimum,
            'PSSMinimum': reference_info.parking_side_setback_minimum,
            'PSSSMinimum': reference_info.parking_street_setback_minimum,
            'RAPDMinimum': reference_info.recreation_area_minimum,
            'LCRSMax': reference_info.low_coverage_maximum
                }   
        }   
    }
}