<template>
  <div className="max-w-4xl mx-auto p-6">
    <Link className="inline-flex items-center space-x-2 text-blue-600 hover:text-blue-800" href="#">
      <ArrowLeftIcon className="h-5 w-5" />
      <span>Back to Homepage</span>
    </Link>
    <div className="mt-8 flex flex-col lg:flex-row lg:space-x-8">
      <div className="flex-1">
        <h1 className="text-5xl font-bold">Indonesia</h1>
        <div className="mt-4 flex space-x-2">
          <Badge variant="secondary">Republic of Indonesia</Badge>
          <Badge variant="default">Republik Indonesia</Badge>
        </div>
        <div className="mt-6">
          <h2 className="text-lg font-semibold">LatLong</h2>
          <p className="text-2xl font-bold text-blue-600">-5.0, 120.0</p>
        </div>
        <div className="mt-6">
          <h2 className="text-lg font-semibold">Calling Code</h2>
          <p className="text-2xl font-bold text-blue-600">62</p>
          <p className="text-sm text-gray-500">1 country with this calling code</p>
        </div>
      </div>
      <div className="flex-1 mt-8 lg:mt-0">
        <Card className="w-full">
          <CardContent>
            <div className="space-y-4">
              <div>
                <h2 className="text-lg font-semibold">Capital: Jakarta</h2>
              </div>
              <div>
                <h2 className="text-lg font-semibold">Region: Asia</h2>
              </div>
              <div>
                <h2 className="text-lg font-semibold">Subregion: South-Eastern Asia</h2>
              </div>
            </div>
          </CardContent>
        </Card>
        <div className="mt-6">
          <h2 className="text-lg font-semibold">Currency</h2>
          <p className="text-2xl font-bold text-blue-600">IDR</p>
          <p className="text-sm text-gray-500">1 country with this currency</p>
        </div>
      </div>
    </div>
  </div>
</template>
