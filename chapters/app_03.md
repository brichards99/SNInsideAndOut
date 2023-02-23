# Design Patterns

## Widget


	this.getDay = function(config) {
		$http({
			method: 'POST',
			url: '/api/x_8481_maintenance/maintcal/getOutagesByDay',
			data: config
		}).success(function(dat, status) {		
		data.day = dat.result;
		}).error(function(dat, status) {
		});
	};