# Maintainer: BigfootACA <bigfoot@classfun.cn>

_pyname=oslo.policy
_pycname=${_pyname/./-}
pkgname=python-${_pycname}
pkgver=3.7.0
pkgrel=2
pkgdesc="Oslo Policy library"
arch=(any)
url="https://docs.openstack.org/oslo.policy/latest/"
license=(Apache)
depends=(
	python
	python-pbr
	python-requests
	python-oslo-config
	python-oslo-context
	python-oslo-i18n
	python-oslo-serialization
	python-pyaml
	python-stevedore
	python-oslo-utils
)
makedepends=(
	python-setuptools
	python-sphinx
	python-sphinxcontrib-apidoc
	python-openstackdocstheme
	python-reno
)
checkdepends=(
	python-oslotest
	python-requests-mock
	python-stestr
	python-sphinx
	python-coverage
)
options=('!emptydirs')
source=(https://pypi.io/packages/source/${_pyname::1}/$_pyname/$_pyname-$pkgver.tar.gz)
md5sums=('285b1f08d980ee66b09ff9bf6aef0d06')
sha256sums=('966a667aa41983b93472e04e7b7bdf68bef723fc1c8e1223e6011db042492646')
sha512sums=('b4c8ed5e5dccafc68bff54d3ac2b9ea3ed51d930cee23377fbbf731eb3a16faf2c7e41763764002520302cd7c39c78c6011c0748ca151ba5291565443ced5b20')

export PBR_VERSION=$pkgver

build(){
	cd $_pyname-$pkgver
	export PYTHONPATH="$PWD"
	python setup.py build
	sphinx-build -b text doc/source doc/build/text
}

check(){
	cd $_pyname-$pkgver
	stestr run
}

package(){
	cd $_pyname-$pkgver
	python setup.py install --root="$pkgdir/" --optimize=1
	install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
	mkdir -p "$pkgdir/usr/share/doc"
	cp -r doc/build/text "$pkgdir/usr/share/doc/$pkgname"
	rm -r "$pkgdir/usr/share/doc/$pkgname/.doctrees"
}
